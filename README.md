# assisted-service-helm

Helm charts for deploying:

* https://github.com/openshift/assisted-service/
* https://github.com/openshift-assisted/assisted-ui

## How to do it

In your values.yaml set your database settings, using an external database is not 
yet supported.

```
postgresql:
  postgresqlDatabase: "installer"
  postgresqlUsername: "admin"
  postgresqlPassword: "admin"
```

In you values.yaml set the configuration, for example:

```
config:

  # Generate dummy ignition configs.
  DUMMY_IGNITION: false

  # List of releases and the path to the release image.
  OPENSHIFT_VERSIONS: '{"4.6":{"display_name":"4.6.16","release_version":"4.6.16","release_image":"quay.io/openshift-release-dev/ocp-release:4.6.16-x86_64","rhcos_image":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.6/4.6.8/rhcos-4.6.8-x86_64-live.x86_64.iso","rhcos_rootfs":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.6/4.6.8/rhcos-live-rootfs.x86_64.img","rhcos_version":"46.82.202012051820-0","support_level":"production"},"4.7":{"display_name":"4.7.33","release_version":"4.7.33","release_image":"quay.io/openshift-release-dev/ocp-release:4.7.33-x86_64","rhcos_image":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.7/4.7.33/rhcos-4.7.33-x86_64-live.x86_64.iso","rhcos_rootfs":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.7/4.7.33/rhcos-live-rootfs.x86_64.img","rhcos_version":"47.84.202109241831-0","support_level":"production"},"4.8":{"display_name":"4.8.14","release_version":"4.8.14","release_image":"quay.io/openshift-release-dev/ocp-release:4.8.14-x86_64","rhcos_image":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.8/4.8.14/rhcos-4.8.14-x86_64-live.x86_64.iso","rhcos_rootfs":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.8/4.8.14/rhcos-live-rootfs.x86_64.img","rhcos_version":"48.84.202109241901-0","support_level":"production","default":true},"4.9":{"display_name":"4.9.0","release_version":"4.9.0","release_image":"quay.io/openshift-release-dev/ocp-release:4.9.0-x86_64","rhcos_image":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.9/4.9.0/rhcos-4.9.0-x86_64-live.x86_64.iso","rhcos_rootfs":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.9/4.9.0/rhcos-live-rootfs.x86_64.img","rhcos_version":"49.84.202110081407-0","support_level":"production"}}'

  # Operating syste mimages and the URL for generating ISO
  OS_IMAGES: '[{"openshift_version":"4.6","cpu_architecture":"x86_64","url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.6/4.6.8/rhcos-4.6.8-x86_64-live.x86_64.iso","rootfs_url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.6/4.6.8/rhcos-live-rootfs.x86_64.img","version":"46.82.202012051820-0"},{"openshift_version":"4.7","cpu_architecture":"x86_64","url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.7/4.7.33/rhcos-4.7.33-x86_64-live.x86_64.iso","rootfs_url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.7/4.7.33/rhcos-live-rootfs.x86_64.img","version":"47.84.202109241831-0"},{"openshift_version":"4.8","cpu_architecture":"x86_64","url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.8/4.8.14/rhcos-4.8.14-x86_64-live.x86_64.iso","rootfs_url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.8/4.8.14/rhcos-live-rootfs.x86_64.img","version":"48.84.202109241901-0"},{"openshift_version":"4.9","cpu_architecture":"x86_64","url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.9/4.9.0/rhcos-4.9.0-x86_64-live.x86_64.iso","rootfs_url":"https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.9/4.9.0/rhcos-live-rootfs.x86_64.img","version":"49.84.202110081407-0"},{"openshift_version":"4.9","cpu_architecture":"arm64","url":"https://mirror.openshift.com/pub/openshift-v4/aarch64/dependencies/rhcos/4.9/4.9.0/rhcos-4.9.0-aarch64-live.aarch64.iso","rootfs_url":"https://mirror.openshift.com/pub/openshift-v4/aarch64/dependencies/rhcos/4.9/4.9.0/rhcos-4.9.0-aarch64-live-rootfs.aarch64.img","version":"49.84.202110080947-0"}]'

  # OCP release version
  RELEASE_IMAGES: '[{"openshift_version":"4.6","cpu_architecture":"x86_64","url":"quay.io/openshift-release-dev/ocp-release:4.6.16-x86_64","version":"4.6.16"},{"openshift_version":"4.7","cpu_architecture":"x86_64","url":"quay.io/openshift-release-dev/ocp-release:4.7.33-x86_64","version":"4.7.33"},{"openshift_version":"4.8","cpu_architecture":"x86_64","url":"quay.io/openshift-release-dev/ocp-release:4.8.14-x86_64","version":"4.8.14","default":true},{"openshift_version":"4.9","cpu_architecture":"x86_64","url":"quay.io/openshift-release-dev/ocp-release:4.9.0-x86_64","version":"4.9.0"},{"openshift_version":"4.9","cpu_architecture":"arm64","url":"quay.io/openshift-release-dev/ocp-release:4.9.0-aarch64","version":"4.9.0"}]'

  # For single node deployments
  ENABLE_SINGLE_NODE_DNSMASQ: true

  # Where public container images are located
  PUBLIC_CONTAINER_REGISTRIES: quay.io

  # ?
  NTP_DEFAULT_SERVER: "ntp1.anu.edu.au"

  # Enable IPV6
  IPV6_SUPPORT: true
  AUTH_TYPE: none
  HW_VALIDATOR_REQUIREMENTS: '[{"version":"default","master":{"cpu_cores":4,"ram_mib":16384,"disk_size_gb":120,"installation_disk_speed_threshold_ms":10,"network_latency_threshold_ms":100,"packet_loss_percentage":0},"worker":{"cpu_cores":2,"ram_mib":8192,"disk_size_gb":120,"installation_disk_speed_threshold_ms":10,"network_latency_threshold_ms":1000,"packet_loss_percentage":10},"sno":{"cpu_cores":8,"ram_mib":32768,"disk_size_gb":120,"installation_disk_speed_threshold_ms":10}}]'
  ENABLE_AUTO_ASSIGN: "true"

  # Change to your needs
  SERVICE_BASE_URL: "https://assisted-ui.apps.k8s.hahl.id.au"
  ASSISTED_SERVICE_URL: "https://assisted-api.apps.k8s.hahl.id.au"
```

You might also like to change:
```

mirror_registry:
  ca_bundle: |
    -----BEGIN CERTIFICATE-----
    <certificate>
    -----END CERTIFICATE-----

  registries_conf: |
    unqualified-search-registries = ["registry.access.redhat.com", "docker.io"]

    [[registry]]
      prefix = ""
      location = "quay.io/ocpmetal"
      mirror-by-digest-only = false

     [[registry.mirror]]
       location = "mirror1.registry.corp.com:5000/ocpmetal"
```

 Then deploy.
