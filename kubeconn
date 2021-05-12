#!/usr/bin/env bash

conn(){
  #show up namespaces and select
  echo ""
  kubectl get namespaces | tail --lines=+2 | awk '{print NR " " $1}'
  echo -en "\nPlease select namespace <Press Enter to 'default'>: "
  read select
  if [[ $select = "" ]]; then
    NAMESPACE='default'
  else
    NAMESPACE=$(kubectl get namespaces | tail --lines=+2 | awk '{print $1}' | awk NR==$select)
  fi

  #Check available Pod
  NUM_POD=$(kubectl get pods -n $NAMESPACE | tail --lines=+2 | awk '{print $1}' | wc -l)
  if [[ $NUM_POD = 0 ]]; then
    exit 0
  fi

  #Show up pod and select
  kubectl get pods -n $NAMESPACE | tail --lines=+2 | awk '{print NR " " $1}'
  echo -en "\nPlease select pod in <$NAMESPACE>: "
  read select
  POD=$(kubectl get pods -n $NAMESPACE | tail --lines=+2 | awk '{print $1}' | awk NR==$select)
  NUM_POD=$(kubectl get pods -n $NAMESPACE | tail --lines=+2 | awk '{print $1}' | wc -l)

  #single or multi container
  NUM_CONT=$(kubectl describe pod -n $NAMESPACE $POD | grep -B 1 "Container ID" | egrep -v "Container|--" | wc -l)

  if [[ $NUM_CONT > 1 ]]; then
    kubectl describe pod -n $NAMESPACE $POD | grep -B 1 "Container ID" | egrep -v "Container|--" | awk -F":" '{print NR $1}'
    echo -en "\nPlease select container in <$POD>: "
    read select
    CONTAINER=$(kubectl describe pod -n $NAMESPACE $POD | grep -B 1 "Container ID" | egrep -v "Container|--" | awk -F":" '{print $1}' | awk NR==$select)
    kubectl exec -it -n $NAMESPACE $POD -c $CONTAINER -- /bin/sh;
  else
    kubectl exec -it -n $NAMESPACE $POD -- /bin/sh;
  fi
}

conn # call function