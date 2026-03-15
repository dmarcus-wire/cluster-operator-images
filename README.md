# Operators to install

For OpenShift 4.20.4/12 Environment

## Multi-Cluster Management & Security

1. **Advanced Cluster Management for Kubernetes** 2.16.0 - Manages multiple OpenShift/Kubernetes clusters from a single hub, including policy enforcement, application lifecycle, observability across clusters, and multicluster governance.
1. **Advanced Cluster Security for Kubernetes** 4.10.0 - Provides runtime security, vulnerability scanning, compliance monitoring, network segmentation, and threat detection for containers and Kubernetes workloads (formerly StackRox).
1. **cert-manager Operator for Red Hat OpenShift** 1.18.1 - Automates the management and issuance of TLS certificates from various issuers (e.g., Let's Encrypt, self-signed, Vault), handling renewals and injection into pods/services.
1. **File Integrity Operator** 1.3.8 - Continuously monitors node file integrity using AIDE (Advanced Intrusion Detection Environment), detecting unauthorized changes to critical system files for security hardening and compliance.
1. **Compliance Operator** 1.8.2 - Automates security compliance scanning and remediation using OpenSCAP profiles (e.g., for CIS, PCI-DSS, HIPAA), generating reports and applying remediations to meet regulatory standards.
1. **Gatekeeper Operator** 3.20.0 - Enforces policy-as-code using Open Policy Agent (OPA) Gatekeeper, validating and mutating Kubernetes resources to enforce security, best practices, and custom constraints cluster-wide.
1. **multicluster engine for Kubernetes** 2.11.0 - Provides foundational multicluster management capabilities (often a dependency for ACM), enabling hub-spoke cluster orchestration, placement policies, and lifecycle management across environments.

## Observability

1. **Cluster Observability Operator** 1.3.1 - Enables creation and management of customizable, standalone monitoring stacks (e.g., Prometheus, Thanos, Alertmanager) for detailed namespace-level observability, beyond the default cluster monitoring, with console integration for metrics/logs/traces correlation.
1. **Loki Operator** 6.4.3 - Deploys and manages LokiStack (a secure, multi-tenant Loki deployment) as a log storage backend, integrated with OpenShift authentication, for scalable log aggregation and querying.
1. **Package Server** 0.0.1-snapshot - An internal OLM component that serves as a catalog server, exposing Operator metadata from catalogs to the OperatorHub UI and oc CLI for discovery and installation.
1. **Power monitoring for Red Hat OpenShift** 0.5.0 - Collects and exposes energy/power consumption metrics (e.g., via RAPL interfaces) for nodes and containers, enabling power usage monitoring, optimization, and reporting in Prometheus.
1. **Red Hat build of OpenTelemetry** 0.144.0-1 - Deploys OpenTelemetry Collectors to collect, process, and export telemetry data (metrics, logs, traces) in OTLP format, supporting integration with backends like Prometheus, Loki, Tempo.
1. **Red Hat OpenShift Logging** 6.4.3 - Collects, forwards, stores, and visualizes container and node logs using collectors (Vector), with support for LokiStack or other backends, and console integration for log querying.
1. **Red Hat Service Interconnect Network Observer** 2.1.3-rh-1 - (Likely the Network Observability Operator under a specific branding/variant) — Collects network flow data using eBPF, visualizes traffic topology, detects anomalies, and stores flows (often in Loki) for network troubleshooting and security.
1. **Tempo Operator** 0.20.0-1 - Deploys and manages Tempo (Grafana Tempo) as a scalable, cost-effective distributed tracing backend, supporting ingestion of traces (Jaeger, Zipkin, OTLP) and querying/visualization.

## Operations

1. **OpenShift Lightspeed Operator** 1.0.10 - Powers AI-assisted features in the OpenShift console (e.g., natural language queries, troubleshooting suggestions, code generation), using generative AI for developer and admin productivity.
1. **Red Hat OpenShift Service Mesh** 3 3.2.2 - Provides Istio-based service mesh for traffic management, security (mTLS), observability (metrics/tracing), and policy enforcement across microservices.
1. **Web Terminal** 1.15.0 - Provides secure, browser-based terminal access to the cluster for developers/admins, with ephemeral pods for shell sessions, no need for local kubectl.
1. **DevWorkspace Operator** 0.39.0 - Manages cloud-native developer workspaces (based on Eclipse Che/Dev Spaces), providing isolated, containerized development environments accessible via browser, with IDE integration.
1. **Red Hat OpenShift Pipelines** 1.21.0 - Implements Tekton for cloud-native CI/CD pipelines as code, enabling automated builds, tests, deployments, and workflows using Kubernetes-native resources.
1. **Red Hat OpenShift Dev Spaces** 3.26.1 - Provides a fully managed, enterprise-ready developer workspace platform (based on Eclipse Che), offering browser-based IDEs, multi-user collaboration, and GitOps workflows.
1. **Red Hat OpenShift GitOps** 1.19.2 - Delivers Argo CD for declarative GitOps continuous delivery, managing application deployments, configurations, and rollouts from Git repositories across clusters.

## Viewing installed operators

```sh
# Command for operators
echo "=== Core Cluster Operators (built-in) ==="
echo "NAME\tVERSION"
oc get co -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.versions[?(@.name=="operator")].version}{"\n"}{end}' | sort

echo -e "\n=== Installed OLM Operators (unique) ==="
echo "DISPLAY NAME\tVERSION"
oc get csv -A -o jsonpath='{range .items[*]}{.spec.displayName}{"\t"}{.spec.version}{"\n"}{end}' | sort -u
```

```
# Expected output
=== Core Cluster Operators (built-in) ===
NAME	VERSION
authentication	4.20.15
baremetal	4.20.15
cloud-controller-manager	4.20.15
cloud-credential	4.20.15
cluster-autoscaler	4.20.15
config-operator	4.20.15
console	4.20.15
control-plane-machine-set	4.20.15
csi-snapshot-controller	4.20.15
dns	4.20.15
etcd	4.20.15
image-registry	4.20.15
ingress	4.20.15
insights	4.20.15
kube-apiserver	4.20.15
kube-controller-manager	4.20.15
kube-scheduler	4.20.15
kube-storage-version-migrator	4.20.15
machine-api	4.20.15
machine-approver	4.20.15
machine-config	4.20.15
marketplace	4.20.15
monitoring	4.20.15
network	4.20.15
node-tuning	4.20.15
olm	4.20.15
openshift-apiserver	4.20.15
openshift-controller-manager	4.20.15
openshift-samples	4.20.15
operator-lifecycle-manager	4.20.15
operator-lifecycle-manager-catalog	4.20.15
operator-lifecycle-manager-packageserver	4.20.15
service-ca	4.20.15
storage	4.20.15

=== Installed OLM Operators (unique) ===
DISPLAY NAME	VERSION
Advanced Cluster Management for Kubernetes	2.16.0
Advanced Cluster Security for Kubernetes	4.10.0
cert-manager Operator for Red Hat OpenShift	1.18.1
Cluster Observability Operator	1.3.1
Compliance Operator	1.8.2
DevWorkspace Operator	0.39.0
File Integrity Operator	1.3.8
Gatekeeper Operator	3.20.0
Loki Operator	6.4.3
multicluster engine for Kubernetes	2.11.0
OpenShift Lightspeed Operator	1.0.10
Package Server	0.0.1-snapshot
Power monitoring for Red Hat OpenShift	0.5.0
Red Hat build of OpenTelemetry	0.144.0-1
Red Hat OpenShift Dev Spaces	3.26.1
Red Hat OpenShift GitOps	1.19.2
Red Hat OpenShift Logging	6.4.3
Red Hat OpenShift Pipelines	1.21.0
Red Hat OpenShift Service Mesh 3	3.2.2
Red Hat Service Interconnect Network Observer	2.1.3-rh-1
Tempo Operator	0.20.0-1
Web Terminal	1.15.0
```

## Mirror ImageSetConfiguration

```sh
kind: ImageSetConfiguration
apiVersion: mirror.openshift.io/v2alpha1
mirror:
  operators:
    - catalog: registry.redhat.io/redhat/redhat-operator-index:v4.20
      packages:
        # Multicluster / Management
        - name: advanced-cluster-management
          defaultChannel: stable-2.16
          channels:
            - name: stable-2.16
              minVersion: 2.16.0
              maxVersion: 2.16.0
        - name: multicluster-engine
          defaultChannel: stable-2.11
          channels:
            - name: stable-2.11
              minVersion: 2.11.0
              maxVersion: 2.11.0

        # Security / Compliance
        - name: advanced-cluster-security
          defaultChannel: stable-4.10
          channels:
            - name: stable-4.10
              minVersion: 4.10.0
              maxVersion: 4.10.0
        - name: compliance-operator
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 1.8.2
              maxVersion: 1.8.2
        - name: file-integrity-operator
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 1.3.8
              maxVersion: 1.3.8
        - name: gatekeeper-operator-product
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 3.20.0
              maxVersion: 3.20.0

        # Observability
        - name: cluster-observability-operator
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 1.3.1
              maxVersion: 1.3.1
        - name: loki-operator
          defaultChannel: stable-6.4
          channels:
            - name: stable-6.4
              minVersion: 6.4.3
              maxVersion: 6.4.3
        - name: tempo-operator
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 0.20.0-1
              maxVersion: 0.20.0-1
        - name: opentelemetry-product
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 0.144.0-1
              maxVersion: 0.144.0-1
        - name: netobserv-operator  # or service-interconnect-network-observer depending on exact bundle
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 2.1.3-rh-1  # Adjust if channel uses different versioning
              maxVersion: 2.1.3-rh-1
        - name: power-monitoring-operator
          defaultChannel: tech-preview  # Often tech-preview in 4.20 era
          channels:
            - name: tech-preview
              minVersion: 0.5.0
              maxVersion: 0.5.0

        # Developer / CI/CD / Mesh
        - name: devworkspace-operator
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 0.39.0
              maxVersion: 0.39.0
        - name: web-terminal
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 1.15.0
              maxVersion: 1.15.0
        - name: openshift-cert-manager-operator
          defaultChannel: stable-v1
          channels:
            - name: stable-v1
              minVersion: 1.18.1
              maxVersion: 1.18.1
        - name: openshift-gitops-operator
          defaultChannel: stable
          channels:
            - name: stable
        - name: openshift-pipelines-operator
          defaultChannel: stable
          channels:
            - name: stable
        - name: servicemeshoperator3  # Red Hat OpenShift Service Mesh 3
          defaultChannel: stable-3.2
          channels:
            - name: stable-3.2
              minVersion: 3.2.2
              maxVersion: 3.2.2
        - name: devspaces
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 3.26.1
              maxVersion: 3.26.1

        # AI / Lightspeed
        - name: openshift-lightspeed-operator
          defaultChannel: stable
          channels:
            - name: stable
              minVersion: 1.0.10
              maxVersion: 1.0.10

  # Optional: Add platform / channels / additionalImages / helm from your gist here
  # platform:
  #   channels:
  #     - name: stable-4.20
  #       type: ocp
  #       minVersion: 4.20.15
  #       maxVersion: 4.20.15
  #       graph: true
```
