---
tags: Uni EST
VL-Date: 15.05.23
---
# GitLab
Die Kollaborationsplattform GitLab hat Continuous [[Integration]] direkt integriert. Hierzu muss man in einem Repository nur ein CI-Config-Datei mit dem Namen .gittlab-cy.yml ablegen. Dies ist eine Textdatei, die die CI Pipeline in der Sprache YAML beschreibt. Es gibt verschiedene Templates, die man auswählen und anpassen kann. Hier das Beispiel, wie man den Gradle Build und Test aus der CI anstossen kann. Dies wird dann in einem GitLab Runner ausgeführt. Dieser Runner ist typischerweise ein Image einer kompletten Ablaufumgebung, die beispielsweise in einem Docker Container ausgeführt wird. Hier sehen wir, dass das vordefinierte Image „gradle:alpine“ verwendet wird. Es ist also ein Alpine Linux, auf dem Gradle (und weitere notwendige Bibliotheken etc.) installiert wurde. GitLab startet dann dieses Image und führt die in der Config vorgegebenen Punkte durch. Im „before_script“ setzen wir Umgebungsparameter. Dann definieren wird die Pipeline. Sie besteht aus den zwei Stufen („Stages“) „build“ und „test“. In der Pipeline laufen dann die beiden gleichnamigen Jobs. Es könnten auch mehrere Jobs einer Stufe zugeordnet werden. Unter „cache“ definieren wir dann noch, welche Teile eines Jobs für den nächsten Lauf gespeichert werden dürfen, damit dieser dann schneller geht. Es gibt natürlich noch viele Möglichkeiten mehr. Details finden Sie hier: https://docs.gitlab.com/ee/ci/yaml/index.html

![[GitLabCIConfigGitlabciyml.png|250]]

## CI Config
- beschreibt, wann etwas zu tun ist
- ruft entsprechende Teile des Build Scripts auf
- kennt die Ablaufumgebung
- Unter Versionskontrolle
In der CI Config beschreiben wir beispielsweise das Betriebsystem (oder die Betriebssysteme), auf der wir den Build und die Tests ausführen oder auch die Datenbanken und zugehörige Passwörter oder sonstige Credentials. Damit ändert sich die CI Config, wenn sich an der Ablaufumgebung etwas ändert, aber das Build Script wird meist unverändert bleiben können.

## Build Script
- beschreibt, was zu tun ist
- kennt die Struktur des Quellcode-Repositorys
- unter Versionskontrolle
Das Build Script kennt hingegen, wie das Quellcode-Repository und der Quellcode aufgebaut ist. Es weiß, was übersetzt werden muss. Es weiß, wo Tests sind, die ausgeführt werden müssen. Wenn ich also meine Tests in Unterverzeichnisse für Unit-Tests und Integrationstests aufteile, dann muss sich das Build Script ändern. Die CI Config sollte davon aber nicht betroffen sein.

## Erweiterung der .gitlab-ci.yml
![[gitlabcode.png|300]]

Die Erweiterung unseres CI-Skripts in Anlehnung an https://gitlab.com/gitlab-examples/spring-gitlab-cf-deploydemo/-/tree/master/docs Wir schieben bei Änderungen im main branch die neuen Binaries in die Cloud-Produktionsumgebung.
