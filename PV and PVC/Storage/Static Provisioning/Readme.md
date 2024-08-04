# Static Provisioning: -
In this provisioning method, we create PV's manually and then we instruct PVC's to fetch the PV for Kubernetes.

## Benefits of using Static Provisioning: 
- **Control**- We will have the full control over the storage configuration.
- **Predictability**- We can have precise/exact storage setup.
- **Enviroments**- We ideally use this for test and development environments.
- **Legacy System**- This Provisioning used for Legacy System (Which require manual configurations). Example: - If the organization which is invested storages and already have the infrastructure setup.


## Drawbacks of using Static Provisioning:
