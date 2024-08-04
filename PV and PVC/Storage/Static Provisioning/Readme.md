# Static Provisioning: -
In this provisioning method, we create PV's manually and then we instruct PVC's to fetch the PV for Kubernetes.

## Benefits of using Static Provisioning: 
- **Control**- We will have the full control over the storage configuration.
- **Predictability**- We can have precise/exact storage setup.
- **Enviroments**- We ideally use this for test and development environments.
- **Legacy System**- This Provisioning used for Legacy System (Which require manual configurations). Example: - If the organization which is invested storages and already have the infrastructure setup.


## Drawbacks of using Static Provisioning:
- **Manual Management**- Requires manual intervention to create and manage PVs. And this can lead to many errors as the number PVs and PVCs grows.
- **Scalability**- As your storage needs increase, manually managing PVs can become difficult.
- **Complexity**- More complex to manage compared to dynamic provisioning.
- **Resource Allocation**- You need to ensure that there are enough available PVs to meet PVC requests. If you run out of PVs or they don’t match the PVC requirements, it can lead to issues.
- **Consistency**- There’s a risk of inconsistency if PVs are not properly created or if there’s a mismatch between PV specifications and PVC requests.
