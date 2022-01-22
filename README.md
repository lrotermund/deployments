# K8S practice cluster

## Seal a secret

The following steps describe, how to generate a sealed secret: [kubectl-commands > secret generic](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-secret-generic-em-)

1. Generate the source secret file
    * From raw data
    ```sh
    kubectl create secret generic my-secret --dry-run=client --from-literal=name=secretname --from-literal=password=topsecret -o yaml > my-secret.yaml
    ```

    * From a file:
    ```sh
    kubectl create secret generic my-secret --dry-run=client --from-file=mysecret=path/to/mysecret -o yaml > my-secret.yaml
    ```

2. Seal the previously generated secret file
```sh
kubeseal --format yaml < my-secret.yaml > my-sealedsecret.yaml
```

3. Cleanup

Remove the raw secret carefully so that it is not versioned by git. Last but not least add the sealed secret to git. 

