## Kurze Beschreibung was Kubernetes ist

Kubernetes ist eine Open-Source-Plattform zur Orchestrierung, Verwaltung und Automatisierung von containerisierten Anwendungen. Es ermöglicht das Verwalten und Skalieren von Anwendungen über mehrere Hosts und stellt dabei Funktionen wie automatische Bereitstellung, Load Balancing, Self-Healing und Rollbacks bereit.

## Kurze Beschreibung was Microservices sind

Microservices sind eine Architektur, bei der eine Anwendung aus mehreren kleinen, unabhängigen Diensten besteht, die jeweils eine spezifische Aufgabe erfüllen. Jeder Microservice ist eigenständig deploybar, häufig um eine eigene Datenbank und API herum gebaut, und kann unabhängig entwickelt, getestet und skaliert werden.

## Vergleich lightweight Kubernetes Anwendungen

| Anwendung                | Kurzbeschreibung                                                                                 |
|--------------------------|--------------------------------------------------------------------------------------------------|
| **minikube**             | [minikube](https://github.com/kubernetes/minikube) eignet sich zum schnellen „Luft Schnuppern“ von Kubernetes. Es bietet eine Single Node Umgebung und ist ideal zum Ausprobieren und Lernen. |
| **microk8s**             | [microk8s](https://microk8s.io/docs) von Canonical (für Ubuntu) ist das kleinste, schnellste und vollständig konforme Kubernetes System. Besonders für Entwickler und IoT geeignet. |
| **kubeadm**              | [kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/) ermöglicht das Setup von Single Node bis zu hochverfügbaren (HA) Kubernetes Clustern. |
| **Docker for Windows**   | [Docker for Windows](https://docs.docker.com/desktop/install/windows-install/) enthält eine einfache Kubernetes-Integration für lokale Entwicklungszwecke auf Windows Maschinen. |
| **kind**                 | [kind](https://kind.sigs.k8s.io/) (Kubernetes IN Docker) ermöglicht das Ausführen von Kubernetes Clustern als Docker Container, ideal für Tests und CI/CD Workflows. |
| **k3s**                  | [k3s](https://k3s.io/) ist eine ultraleichte Kubernetes-Distribution, speziell entwickelt für ressourcenschwache Umgebungen wie Edge und IoT. |
