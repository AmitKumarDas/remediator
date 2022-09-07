## Deployment Artifacts
This folder hosts various yamls needed to apply remediator controller on a Kubernetes cluster

_Note: kube-system namespace is used for this deployment_

### CLI arguments

#### Generic
```shell
--enable-leader-election                                        Enable leader election for controller manager. Enabling this will ensure there is only one active controller manager.
--health-addr string                                            The address the health endpoint binds to. (default ":9440")
--kube-api-burst int                                            The maximum burst queries-per-second of requests sent to the Kubernetes API. (default 100)
--kube-api-qps float32                                          The maximum queries-per-second of requests sent to the Kubernetes API. (default 50)
--leader-election-lease-duration duration                       Interval at which non-leader candidates will wait to force acquire leadership (duration string). (default 35s)
--leader-election-release-on-cancel                             Defines if the leader should step down voluntarily on controller manager shutdown. (default true)
--leader-election-renew-deadline duration                       Duration that the leading controller manager will retry refreshing leadership before giving up (duration string). (default 30s)
--leader-election-retry-period duration                         Duration the LeaderElector clients should wait between tries of actions (duration string). (default 5s)
--log-encoding string                                           Log encoding format. Can be 'json' or 'console'. (default "json")
--log-level string                                              Log verbosity level. Can be one of 'trace', 'debug', 'info', 'error'. (default "info")
--max-retry-delay duration                                      The maximum amount of time for which an object being reconciled will have to wait before a retry. (default 15m0s)
--metrics-addr string                                           The address the metric endpoint binds to. (default ":8080")
--min-retry-delay duration                                      The minimum amount of time for which an object being reconciled will have to wait before a retry. (default 750ms)
--watch-all-namespaces                                          Watch for custom resources in all namespaces, if set to false it will only watch the runtime namespace.
```

#### Controller specific
```shell
--vagc-disable-volumeattachment-reconciler                      Disables VolumeAttachment garbage collect controller
--vagc-garbage-collect-on-node-not-ready                        Enables garbage collection when Node Ready condition is false or unknown. Dependent on vagc-min-age-node-condition-type-ready
--vagc-matching-csi-attachers strings                           List of CSI attachers whose VolumeAttachments will be considered for garbage collection (default [csi.vsphere.vmware.com])
--vagc-matching-external-attacher-finalizers strings            List of external-attacher finalizer(s) that will be considered for removal (default [external-attacher/csi-vsphere-vmware-com])
--vagc-matching-node-taint-keys strings                         Node taint key(s) that enable garbage collection. Dependent on vagc-min-age-node-condition-type-ready
--vagc-matching-node-taint-keys-with-no-execute strings         Node taint key(s) with NoExecute effect that enable garbage collection. Dependent on vagc-min-age-node-taint-keys-with-no-execute
--vagc-max-concurrent-reconciles int                            Maximum number of concurrent reconciles that will be run (default 1)
--vagc-min-age-node-condition-type-ready duration               Minimum duration for the Node Ready condition value to remain unchanged (default 10m0s)
--vagc-min-age-node-taint-keys-with-no-execute duration         Minimum age of each Node taint key(s) with NoExecute effect (default 10m0s)
--vagc-min-delay-remove-external-attacher-finalizers duration   Delay removal of external-attacher finalizer(s)
```

#### Defaults
Note: Following defaults are represented as code (_hence cannot be copied as yaml values_)

```go
var (
    DisableVolumeAttachmentReconciler        = false
    MatchingCSIAttachers                     = []string{"csi.vsphere.vmware.com"}
    MinAgeNodeConditionTypeReady             = time.Minute * 10
    GarbageCollectOnNodeNotReady             = false
    MatchingNodeTaintKeys                    = []string{""}
    MatchingNodeTaintKeysWithNoExecute       = []string{""}
    MinAgeNodeTaintKeysWithNoExecute         = time.Minute * 10
    MinDelayRemoveExternalAttacherFinalizers = time.Minute * 5
    MatchingExternalAttacherFinalizers       = []string{"external-attacher/csi-vsphere-vmware-com"}
    MaxConcurrentReconciles                  = 1
)
```
