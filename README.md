# manage-versioning-deployments-helm

Rollout commands in Kubernetes deployments are used to manage the deployment of new versions of your application. These commands allow you to update, rollback, or check the status of your deployments. Here are some commonly used rollout commands:

1. **Check the status of a deployment rollout:**
   ```
   kubectl rollout status deployment/<deployment_name>
   ```

2. **Roll out an update to a deployment:**
   ```
   kubectl set image deployment/<deployment_name> <container_name>=<new_image_name>
   ```

3. **Rollback to the previous version of a deployment:**
   ```
   kubectl rollout undo deployment/<deployment_name>
   ```

4. **Rollback to a specific revision of a deployment:**
   ```
   kubectl rollout undo deployment/<deployment_name> --to-revision=<revision_number>
   ```

5. **Pause a deployment rollout:**
   ```
   kubectl rollout pause deployment/<deployment_name>
   ```

6. **Resume a paused deployment rollout:**
   ```
   kubectl rollout resume deployment/<deployment_name>
   ```

7. **View rollout history:**
   ```
   kubectl rollout history deployment/<deployment_name>
   ```

8. **View detailed information about a specific revision:**
   ```
   kubectl rollout history deployment/<deployment_name> --revision=<revision_number>
   ```
## helm

The `helm upgrade` command is used to upgrade a Helm release to a new version or configuration. It's a fundamental command in Helm for managing releases. Here's the basic syntax:

```
helm upgrade [RELEASE] [CHART] [flags]
```

- `[RELEASE]` is the name you've given to the release you want to upgrade.
- `[CHART]` is the name of the chart you want to upgrade to, or the path to the chart directory.
- `[flags]` are optional flags you can use to customize the upgrade process, such as setting values or specifying a namespace.

For example, to upgrade a release named "myapp" to the latest version of a chart named "mychart", you would execute:

```
helm upgrade myapp mychart
```

You can also include additional flags to customize the upgrade process. For instance, if you want to set specific values during the upgrade, you can use the `--set` flag:

```
helm upgrade myapp mychart --set key1=value1,key2=value2
```

This command would upgrade the "myapp" release using the "mychart" chart and set the values of `key1` and `key2` to `value1` and `value2` respectively.
### Example

Suppose you have a chart named `wordpress` with a `values.yaml` file that includes configuration options like database credentials, service type, and replica count.

Your `values.yaml` might look something like this:

```yaml
wordpress:
  image: wordpress:5.8.2
  database:
    user: wpuser
    password: wppassword
    name: wpdb
  service:
    type: LoadBalancer
  replicaCount: 3
```

Now, let's assume you want to upgrade your WordPress application to version 5.9.0 and change the service type to `ClusterIP` while maintaining the existing database credentials. You can achieve this with the following `helm upgrade` command:

```bash
helm upgrade myapp wordpress --set wordpress.image=wordpress:5.9.0,wordpress.service.type=ClusterIP
```

This command will upgrade the Helm release named `myapp` to use the `wordpress` chart, setting the image to `wordpress:5.9.0` and changing the service type to `ClusterIP`, while keeping the existing database credentials and other configuration values intact.

### Helm rollback

In Helm, the package manager for Kubernetes, the rollback command is used to revert a release to a previous version. This is particularly useful if a recent deployment introduces issues or unexpected behavior, and you need to quickly revert to a stable version. Here's the syntax for the Helm rollback command:

```
helm rollback <release_name> <revision_number>
```

Where:
- `<release_name>` is the name of the Helm release you want to rollback.
- `<revision_number>` is the revision number you want to rollback to. Each release in Helm is assigned a revision number, which indicates the version of the release.

For example, if you want to rollback the release named "myapp" to the third revision, you would execute:

```
helm rollback myapp 3
```
