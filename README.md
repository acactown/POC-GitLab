# POC-GitLab


## Introducción

Simple POC de integración de GitLab, Jenkins y Sonarqube.

Made with all :heart: by `acactown`.


## Versión

Current Version: **1.0.0**


## Prerequisitos

You will need the following things properly installed on your computer.

* [Git](http://git-scm.com/)
* [Docker](https://docs.docker.com/userguide/)
* [Docker Compose](https://docs.docker.com/compose/install/)
* [Java](http://nodejs.org/)


## Instalación

**1. Clonar el repositorio**
```bash
git clone git@github.com:acactown/POC-GitLab.git
```

**2. Cambiarse de directorio `POC-GitLab`**
```bash
cd POC-GitLab
```

**3. Generar los volúmenes de Docker**
```bash
cat volumes* > volumes.zip
```

**4. Descomprimir los volúmenes de Docker**
```bash
unzip volumes.zip
```

**5. Editar el archivos de host `/etc/hosts`**
```
127.0.0.1    jenkins
127.0.0.1    gitlab
127.0.0.1    sonarqube
```

**6. Deshabilitar config de proxy para host de Docker  `/etc/environment`**
```
NO_PROXY="localhost,127.0.0.1,jenkins,gitlab,sonarqube"
```

**7. Agregar SSH Keys**
```bash
cp ./ssh/* ~/.ssh/
```

**8. Editar archivo de SSH config**
```
Host gitlab 
    HostName gitlab
    user aamadoc
    IdentityFile ~/.ssh/gitlab_rsa
```

## Ejecución

**1. Ejecutar `docker-compose`**
```bash
docker-compose up
```

**2. Esperar a que baje las imágenes de Docker y arranquen los container...**

**3. Probar que todo subió con éxito:**

   * **Jenkins:** http://jenkins/
      	* user: aamadoc
      	* pwd: pslabc123 
      	
   * **Gitlab:** http://gitlab/
   	  	* user: aamadoc
      	* pwd: pslabc123
      	
   * **Sonarqube:** http://sonar/
   		* user: admin
      	* pwd: pslabc123


## Configuración de GitLab

**1. Crear un proyecto:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/new-project.png)
---

**2. Proyecto creado:**
![Proyecto creado](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/created-project.png)
---

**3. Importar code de test:**
![Proyecto importado](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/readme-project.png)
---


## Configuración de Jenkins

**1. Agregar credenciales SSH y GitlLab Token:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/jenkins-credentials.png)
---

**2. Crear un job:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/config-job-jenkins.png)
---

**3. Config de build del job:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/config-build-jenkins.png)
---

**4. Ejecutar build:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/build-success.png)
---


## Configuración de Sonar

**1. Instalar plugin Java y Gitlab comment:**
*URL Plugin:* https://gitlab.talanlabs.com/gabriel-allaigre/sonar-gitlab-plugin
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/sonar-plugin.png)
---

**2. Revisar proyecto:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/sonar-project.png)
---


## Crear MR de GitLab

**1. Clonar el repositorio:**
```bash
git clone ssh://git@gitlab:10022/aamadoc/fortune-teller.git
```

**2. Realizar crear branch de prueba y agregar cambios de prueba:**
```bash
git checkout -b add-fortune-picker
git push origin add-fortune-picker
```
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/static-code-error.png)
---

**3. Crear un MR para probar la integración con Sonarqube:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/created-mr.png)
---

**2. Ejecución automatica del Job de Jenkins:**
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/gradle-console-log.png)
---

**3. Comentarios generados por Sonarqube Gitlab publisher:**

Está utilizando mi token personal, por eso los comentarios quedan a mi nombre :sweat_smile:
![Crear proyecto](https://raw.githubusercontent.com/acactown/POC-GitLab/master/screenshots/mr-comment.png)
---