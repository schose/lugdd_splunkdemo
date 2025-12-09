---

marp: true
theme: default
paginate: true
backgroundImage: url(img/background-std-header.png)

---
<!-- Global style -->
<style>
header {
  color: white;
  background-color: black;
  text-align: right;
  font-size: 30px;
  left: 450px;
  height: 50px;
  top: 10px;
  position: absolute;
  
}

img[alt~="center"] {
  display: block;
  margin: 0 auto;
}

h1 {
  text-align: right;
  font-size: 60px;
}

</style>
<!-- Global style -->

![bg](img/background-chapter.png)


# WTF - Splunk? # 

<!--
- Enterprise / Cloud
- more products like Splunk APM, Splunk DSP, Splunk Oncall (Victorops), Phantom
-->

---
<!--

- big data Plattform
- Umsatz 2021: 2,6 Mrd (Redhat: 3.3Mrd, Citrix: 3.2, Elastic: 0,4 Mrd, Datadog: 0,8 Mrd)
- 6.500 Mitarbeiter

- Strukturiert und undstrukturierte Daten
- Nicht vorhersagbare Formate
- „Single Panes of Glas“

-->
<!-- _header: 'get Data into Splunk' --> 


![w:800px center](img/01-data-import.png) 

--- 

<!-- _header: 'Splunk Roles' --> 

-  Search Head - Search and Reporting * 
![w:200px](img/01-role-searchhead.png)
  -  Indexer – Indexing and Search Service
![w:200px](img/01-role-indexer.png)| 
- Deployment Server / Forwarder Management - Verteilungsmanagement
![w:200px](img/01-role-dpl.png)  
- Forwarder – Indexing and Search Service
![w:200px](img/01-role-forwarder.png)  

<!-- all roles could be installed on a single machine -->

---

<!-- _header: 'Hardware requirements Indexer' --> 

- medium CPU requirements
- medium Memory requirements
- **high IOs requirements**

   - 64Bit OS
   - 12core 2+GHz CPU Cores
   - 12GB  RAM
   - 800 IOPs
   - 1GB NIC

<!-- 
IOPS
Iometer.org
Bonnie++ als HW Benchmark
*/
-->

---

<!-- _header: 'Hardware requirements Search Head' --> 

- **high CPU requirements**

- lower Memory requirements
- medium IOs requirements

   - 64Bit OS
   - **16core** 2+GHz CPU Cores
   - 12GB RAM
   - 800 IOPs
   - 1GB NIC
---

<!-- _header: 'Sizing' --> 

![w:900px center](img/02-sizing.png)

---

<!-- _header: 'single Server Installation' --> 

![w:700px center](img/02-single-server.png)


---

<!-- _header: 'single Server using Universal forwarder' --> 

![w:600px center](img/02-single-server-forwarder.png)

- UFW available for Linux , Mac, Windows, Solaris, FreeBSD, AIX..

---

<!-- _header: 'distributed Enviroment' --> 

![w:600px center](img/02-distributed-env.png)


---

<!-- _header: 'scale out enviroment' --> 

![w:900px center](img/02-largest.png)



---

<!-- _header: 'Scale Out' --> #

![w:500px center](img/01-scaleout.png) 

- horizontal scaling using **MapReduce**

- Load balancing is scaling Indexing

---

<!-- _header: 'areas of application
' --> 

- Application Management
- IT Operations Management
- Security
- Complicance
- Big Data
- (IoT)
  
--- 
![bg](img/background-chapter.png)


# Splunk Apps # 

--- 

<!-- _header: 'Splunk Apps' --> 

![w:400px center](img/01-apps.png) 


- 03/2020 >5000 public Apps

<!--
Wer erstellt Splunk Apps?!

- Vorkonfigurierte Umgebungen die Auf einer Splunkinstanz sitzen
Konzentrieren sich auf einen spezifischen Usecase
Stellen Dashboards, Reports und andere Informationen bereit

Technology Partners (Sendmail Appliance)
Community (ich)
Entwickler (Jason Conger… Citrix) - Splunk
-->

--- 

<!-- _header: 'Splunk Apps' --> 

## who is creating apps? ###

- Technology Partners 
- Community
- Developers
- You!


--- 
![bg](img/background-chapter.png)


# Fragen? # 

