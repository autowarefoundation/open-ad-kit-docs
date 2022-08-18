# How to run Autoware

This page explains how to run Autoware on the development platform that are set up in [the Installation chapter](../installation/index.md).

## Minimum requirements

- Developer Platform: TODO
- In-Vehicle Development Platform [^1]: TODO
- Software Tool: TODO
- Container Image: TODO

[^1]: This is optional if you do NOT need a vehicle-edge platform.

## 1. Run Autoware on the developer platform

### Run Autoware.Auto on AVA platform or PCU

1. Access AVA platform or PCU via SSH.

1. Deploy kubernetes clusters for Autoware.

   ```console
   kubectl apply -f comhpc-deployments
   ```

   :speech_balloon: You can make sure deployments are deployed.

   ```console
   root@comhpc:~# kubectl get deploy -o wide
   NAME               READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES                                                                         SELECTOR
   comhpc-control     1/1     1            1           15h   comhpc       ghcr.io/autowarefoundation/autoware-universe:galactic-20220728-prebuilt-cuda   io.kompose.service=comhpc
   comhpc-api         1/1     1            1           15h   comhpc       ghcr.io/autowarefoundation/autoware-universe:galactic-20220728-prebuilt-cuda   io.kompose.service=comhpc
   comhpc-planning    1/1     1            1           15h   comhpc       ghcr.io/autowarefoundation/autoware-universe:galactic-20220728-prebuilt-cuda   io.kompose.service=comhpc
   comhpc-simulator   1/1     1            1           15h   comhpc       ghcr.io/autowarefoundation/autoware-universe:galactic-20220728-prebuilt-cuda   io.kompose.service=comhpc
   comhpc-map         1/1     1            1           15h   comhpc       ghcr.io/autowarefoundation/autoware-universe:galactic-20220728-prebuilt-cuda   io.kompose.service=comhpc
   comhpc-system      1/1     1            1           17h   comhpc       ghcr.io/autowarefoundation/autoware-universe:galactic-20220728-prebuilt-cuda   io.kompose.service=comhpc
   comhpc-vehicle     1/1     1            1           17h   comhpc       ghcr.io/autowarefoundation/autoware-universe:galactic-20220728-prebuilt-cuda   io.kompose.service=comhpc
   ```

   :speech_balloon: Please make sure all pods are running.

   ```console
   root@comhpc:~# kubectl get pod -o wide
   NAME                                READY   STATUS    RESTARTS   AGE    IP              NODE   NOMINATED NODE   READINESS GATES
   comhpc-control-58cb5b9dbd-fqckv     1/1     Running   0          104m   192.168.10.27   ava    <none>           <none>
   comhpc-api-7b588f7988-n4rb7         1/1     Running   0          103m   192.168.10.27   ava    <none>           <none>
   comhpc-planning-d964b9646-92rzc     1/1     Running   0          104m   192.168.10.27   ava    <none>           <none>
   comhpc-simulator-7f5b9fb97d-7kvqm   1/1     Running   0          104m   192.168.10.27   ava    <none>           <none>
   comhpc-map-7867476c98-mgrm5         1/1     Running   0          103m   192.168.10.27   ava    <none>           <none>
   comhpc-system-c5599d5b-xxhg2        1/1     Running   0          103m   192.168.10.27   ava    <none>           <none>
   comhpc-vehicle-9d6b5b9b8-k95q9      1/1     Running   0          103m   192.168.10.27   ava    <none>           <none>
   ```

## 2. Run Autoware on the in-vehicle development platform

!!! note "If you do NOT need a vehicle-edge platform, please skip this step."

TODO

## 3. Run simulators on the development platform

Please refer to the [How to run simulators](../how-to-run-simulators/index.md) section.
