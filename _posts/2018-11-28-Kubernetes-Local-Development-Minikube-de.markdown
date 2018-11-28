---
layout: post
title: Kubernetes - Lokal Kubernetes Cluster entwickeln und testen mit Minikube
lang: de
ref: kuberneteslocalminikube
date: 2018-11-28 11:45:00 +0300
description: Kubernetes - Lokal Kubernetes Cluster entwickeln und testen mit Minikube
img: kuber-minikube.png
tags: [Kubernetes, Minikube, Local, testing, development environment]
---

# Minikube 
Für das lokale Entwickeln und Testen von Kubernetes Clustern, gibt es eine Platform namens Minikube, die sich lokal installieren lässt.

Im Folgenden installieren wir alles nötige in wenigen Schritten und testen ob die Einrichtung erfolgreich war.

## Windows 10 und Hyper-V (getestet)
Die PowerShell als Administrator starten.
### Step 1: Chocolatey Installieren
Chocolatey ist ein Paket-Manager für Windows.
Den folgenden Befehl ausführen:
```
$ Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
### Step 2: Hyper-V installieren
Den folgenden Befehl ausführen:
```
$ Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V -All
```
Ein Neustart des Rechners ist nun erforderlich.

### Step 3: Minikube und kubernetes-cli installieren
Die folgenden Befehle ausführen:
```
$ choco install minikube
$ choco install kubernetes-cli
```

### Step 4: 
```
# Zum aktivieren des Dashboards
$ minikube addons enable dashboard
```

### Step 5:
In dem Hyper-V Manager müssen wir wie folgt einen Virtuellen Switch Manager für Minikube anlegen.

Actions -> Virtual Switch Manager... -> Create Virtual Switch (External) -> (Name = Minikube Virtual Switch) und (Allow management operating system to share this network adapter = true).

```
# Minikube-VM mit Cluster starten
$ minikube start --vm-driver hyperv --hyperv-virtual-switch "Minikube Virtual Switch"
```
Warten bis das Starten vollständig abgeschlossen ist.

Nun können wir mit dem folgenden Befehl testen ob alles ordnungsgemäß funktioniert hat.
```
# Ausgabe aller Pods des Namespaces kube-system
$ kubectl get pods -n kube-system
```

### Nützliches und Hinweise
Folgend ein paar nützliche Kommandos und Hinweise
```
# Minikube-VM stoppen
$ Minikube stop

# Hängt das Stoppen bei 0%
$ Minikube ssh
$ sudo poweroff

# Aufruf des Kubernetes-Dashboards im Browser
$ minikube dashboard

# Ausgabe aller Services des Namespaces kube-system
$ kubectl get svc --namespace=kube-system

# Auflistung der verfügbaren Addons
$ minikube addons list
```
