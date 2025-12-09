# Using kubectl to interact with the Kubernetes API and configure it for Kyma

### Describe the interaction of kubectl with Kubernetes API

What is kubectl?
To interact with the Kubernetes API, you need a client. The tool kubectl is a command-line tool for interacting with Kubernetes clusters. It allows you to manage and control Kubernetes resources, such as pods, services, deployments, and more. With kubectl, you can perform various operations, including creating, updating, and deleting resources. The Kubernetes API is a REST API, which means that you can interact with it using any HTTP client. Since, you typically also have to deal with authentication and authorization, it is much easier to use a dedicated client like kubectl.

Note

Before diving into the content, we want to point out that if you are interested in SAP BTP, the Kyma runtime, and the kubectl command-line tool, you can find more detailed information in the Learning Journey: Delivering Side-by-Side Extensibility based on SAP BTP, Kyma runtime

Installation and Configuration of Kubectl
Installing Kubectl
The kubectl command-line interface (CLI) must be installed on your local machine. You can install it following the instructions in the official Kubernetes documentation. Scroll down to the further reading section for the link to the official Kubernetes documentation.

Configuring Kubectl
To configure kubectl to point to a specific Kubernetes cluster, you need a kubeconfig file. This file includes important information about your cluster, such as the API server URL, the authentication method, and the certificate authority. The kubeconfig file is usually stored in the home directory of your user account.

For Kyma , along with kubectl, the kubelogin plugin is also required. Read more here.

For example, on Linux, the kubeconfig file is located at ~/.kube/config, and on Windows, you can find it at %USERPROFILE%\.kube\config.

Using Kubectl
Once the kubeconfig file is properly configured, kubectl will use the information from that file to interact with the Kubernetes API when you issue commands. It is also possible to configure kubectl by exporting the kubeconfig file in the terminal. You can use the KUBECONFIG environment variable to specify the location of the kubeconfig file.

Before moving on to commands, remember that everything defined in Kubernetes can be accessed using the RESTful Kubernetes API.

Every command needs to specify the namespace and the object type. If no namespace is specified, the default namespace is used. The object type is the name of the resource type, such as Pods or Deployments. The name of the object is the name of the resource, such as my-pod or my-deployment.

The kubectl syntax is as follows:

kubectl [command] [TYPE] [NAME] [flags]
List Objects
To list objects, you can use the get command. The get command lists one or more resources. For example, to list all Pods in the default namespace, use the following command:

```
kubectl get pods
```

To list all Pods in a specific namespace, you can use the following command:

```
kubectl get pods --namespace my-namespace
```

Note

The --namespace flag is optional. If you don't specify a namespace, the default namespace is used. However, you can also specify the namespace in the kubeconfig file or create different contexts for different namespaces, which you can then switch between or set your custom namespace as default. Read more about contexts in the official Kubernetes documentation.

Here are some other examples of the get command, which lists the resources of a specified type in the default namespace:

```
kubectl get pods
```

```
kubectl get services
```

```
kubectl get replicasets
```

```
kubectl get deployments
```

Create objects
To create objects, you can use the create command. The create command creates a Kubernetes object from a YAML or JSON file. For example, to create a Pod, use the following command:

```
kubectl create -f my-pod.yaml
```

The -f flag is short for --filename. It specifies the path to the YAML or JSON file that contains the object definition.

The create command can also create objects from a URL. For example, to create a Pod from a URL, you can use the following command:

```
kubectl create -f https://raw.githubusercontent.com/SAP-samples/kyma-runtime-learning-journey/main/unit_1/my-pod.yaml
```

Note

If you run the create command twice with the same object definition, it will throw an error. To avoid this, you can use the apply command instead.

Update Objects
To update objects, you can use the apply command. The apply command updates a Kubernetes object from a YAML or JSON file. For example, to update a pod, you can use the following command:

```
kubectl apply -f my-pod.yaml
```

During an apply operation, the Kubernetes API server compares the object definition in the YAML or JSON file with the object's current state in the cluster. If there are any differences, the object is updated.


Delete Objects
To delete objects, you can use the delete command. The delete command deletes a Kubernetes object. For example, to delete a Pod, you can use the following command:

```
kubectl delete pod my-pod
```

Describe Objects

To describe objects, you can use the describe command. The describe command displays detailed information about a Kubernetes object. For example, to describe a Pod, you can use the following command:

```
kubectl describe pod my-pod
```

You can even export the output of the describe command to a YAML or JSON file. For example, to export the output of the describe command to a YAML file, you can use the following command:

```
kubectl describe pod my-pod -o yaml > my-pod.yaml
```

Label Objects
To label objects, you can use the label command. The label command adds or updates labels on a Kubernetes object. For example, to add a label to a pod, you can use the following command:

```
kubectl label pod my-pod my-label=my-value
```

Retrieving Cluster Information
To retrieve cluster information, you can use the cluster-info command. The cluster-info command displays information about the cluster.

```
kubectl cluster-info
```

To retrieve resource usage information, you can use the top command. The top command displays resource usage information for nodes and pods.

```
kubectl top nodes
```

```
kubectl top pods
```

Other Commands
To get a full list of all available commands, you can use the help command.
```
kubectl help
```

Other Clients
The most common way to interact with the Kubernetes API is using kubectl. Kyma, for example, comes with a Dashboard that you can use to interact with the Kubernetes API.

Summary
In this lesson, you learned how to interact with the Kubernetes API using kubectl. You also learned how to configure kubectl and how to use it to list, create, update, delete, and describe objects. You also learned how to label objects and how to get a list of all available commands.

