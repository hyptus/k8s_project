###Autoren: Eberhard Marc, Hangartner Rafael###
###README zum Lab Kubernetes der Gruppe 8###
------------------------------------------------
Informationen: Eine genaue Dokumentation zum Lab wird in Form eines PDFs abegeben, hier bei handelt es sich nur um eine Beschreibung des Zugriffs der einzlenen Komponenten
------------------------------------------------

************************************************
1. Zugriff auf Server
das Passwort wurde uns vom CldInf Team für die Gruppe 8 zur Verfügung gestellt

Mit Terminal mit `ssh ins@sr-000137.network.garden` und durch Eingabe des Passworts

Im Verzeichnis /home/ins/k8s befinden sich alle Konfigurations-Dateien vom Typ YAML, die für den Betrieb von K8s nötig sind. 

Im Verzeichnis /home/ins/helm finden sich alle Konfigurationen die für das Deployment dr DB mit Helm nötig sind.

************************************************

2. Start von K8s
Die Erklärung zum Aufbau der YAML Files, bitte PDF Dokumentation beachten. 

Zur Überprüfung ob die Installation von K8s korrekt ist
`microk8s status --wait-ready` 

Zum erstellen der Namespaces 'kanban' und 'database', wurde folgender Befehl ausgeführt
`kubectl create -f kanban_namesapce.yaml`
`kubectl create -f database_namspace.yaml`

Danach werden alle Dateien die sich im Vrezeichnis /home/ins/k8s/ befinden eingelesen um Services, Pods, Configs und PVC zu erstellen
`kubectl apply -f <filename.yaml>`

Um den Betrieb der Pods zu überprüfen, wird folgender Befehl ausgeführt
`kubectl get pods –all-namespaces`
Nun werde nalle Pods angzeigt und dessen Status
Falls einer dieser Pods in einen Fehler läuft, kann auf dessen Logs zugegriffen werden
Dazu zuerst zum Namespaces des Pods wechseln und durch eingabe des Pod Namen darauf zugreifen
`kubectl config set-context --current --namespace=kanban`
`kubectl get all`
`kubectl logs -f <pod-name>`


Um einen Pod oder Service wieder zu entfernen, kann durch Verwendung des folgenden Befehl
`kubectl delete -f <filename.yaml>`

************************************************

3. Start von Helm DB Deployment
Helm wird im Verzeichnis /home/ins/helm abgelegt, dazu wird die Installationsanleitung von der offziellen Webseite verwendet.

Im File /home/ins/helm/db/values.yaml befinden sich alle Werte für die Installation
Im Verzeichnis /home/ins/helm/db/templates/ finden sich alle Templates, welche mit den Values befüllt werden
Erstellung des Namespace für DB-Helm `kubectl create namespace database-helm`
Zur Installation `helm install -db-env.yaml db ./db`ausführen
Zur Deinistallation `helm unistall db`

(DB läuft aktuell auf Server, Kanban-App ist aber nicht mehr an ihr angehängt) 

************************************************

4. Zugriff Web
Über den Webbrowser ist die Webseite nach Start der Container im Kubernetes über folgende Adresse erreichbar: http://sr-000137.network.garden/


************************************************

