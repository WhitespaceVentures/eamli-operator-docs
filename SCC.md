# SecurityContextConstraints

```
apiVersion: security.openshift.io/v1
kind: SecurityContextConstraints
metadata:
  annotations:
    kubernetes.io/description: 'eamli-service is designed to be used by all
    Eamli services installed by the Eamli Operator.'
  creationTimestamp: null
  name: eamli-service
allowHostDirVolumePlugin: false
allowHostIPC: false
allowHostNetwork: false
allowHostPID: false
allowHostPorts: false
allowPrivilegeEscalation: false
allowPrivilegedContainer: false
allowedCapabilities: []
defaultAddCapabilities: []
fsGroup:
  type: MustRunAs
priority: 10
readOnlyRootFilesystem: false
requiredDropCapabilities:
- ALL
runAsUser:
  type: MustRunAs
  uid: 1000650001
seLinuxContext:
  type: MustRunAs
seccompProfiles: ['docker/default']
supplementalGroups:
  type: MustRunAs
  ranges:
  - min: 1000650001
    max: 1000650001
volumes:
- configMap
- downwardAPI
- emptyDir
- persistentVolumeClaim
- projected
- secret
```
