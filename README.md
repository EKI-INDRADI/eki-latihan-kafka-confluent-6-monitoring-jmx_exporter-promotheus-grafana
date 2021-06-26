# Eki Indradi monitoring Confluent Config 

Research & development 2021

# Confluent 6 monitoring - Prometheus & Grafana  - Multi JMX_EXPORTER :

ini adalah rangkuman dari penelitian saya yang berhasil untuk monitoring 
confluent 6 kafka server menggunakan prometheus dan grafana dengan bantuan jmx exporter

jika anda copas penelitan ini mohon lampirkan sumbernya bahkan 
orang bule pun belum ada yang share untuk monitoring ini (dengan sempurna)
jujur ini sangat mahal, karena waktu riset saya cukup lama 


====== CONFLUENT SERVER CONFIG

system requirement : 

- Ubuntu server 18.04 LTS (x64)

- MULTI JVM (JDK/JRE 11)

- Confluent 6

- Jmx Exporter

- Prometheus

- Grafana



====== Install java

Ubuntu :

apt-get update

apt-get install default-jdk  (ubuntu 1804 default = jdk 11, ubuntu 1604 default = jdk 8)

apt-get install openjdk-8-jdk

apt-get install openjdk-11-jdk


Manual :

https://jdk.java.net/archive/


curl -L -o openjdk-11.0.2_linux-x64_bin.tar.gz https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz

untuk tutorial multi java 11 dapat di lihat pada :


Note : kenapa multi java ? karena setiap agent service dari JMX_EXPORTER membutuhkan 1 jvm, 

untuk mengeluarkan metrics prometheus, jika di gabung semua service JMX_EXPORTER akan error


di ibaratkan keperluan sebagai berikut : 

https://github.com/EKI-INDRADI/eki-latihan-multi-java-ubuntu-server-1804-lts


apt-get install default-jdk -> untuk control center

cp -avr jdk-11.0.2 jdk-11.0.2-clone1 --> untuk zookeeper

cp -avr jdk-11.0.2 jdk-11.0.2-clone2 --> untuk kafka

cp -avr jdk-11.0.2 jdk-11.0.2-clone3 --> untuk connect

jdk-11.0.2 --> cadangan

===== Download JMX_EXPORTER

curl -L -o jmx_prometheus_javaagent-0.14.0.jar https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.14.0/jmx_prometheus_javaagent-0.14.0.jar




===== JMX_EXPORTER Example

https://github.com/prometheus/jmx_exporter/tree/master/example_configs





==== Step

1. Install multi java 
2. Config Confluent with multi java & config JMX_EXPORTER example (kafka-run-class* ,zookeeper-server-start , kafka-server-start, connect-distributed), 
3. Run Confluent (confluent local services start)

==== / CONFLUENT SERVER CONFIG








==== PROMETHEUS SERVER CONFIG

system requirement :

- Ubuntu server 18.04 LTS (x64)

- JDK 11

- Grafana 7.3.7 (Open Source Edition)

- Prometheus 2.24.0

- Node Exporter 1.0.1




==== Prometheus Config :

https://devopscube.com/install-configure-prometheus-linux/

https://computingforgeeks.com/install-prometheus-server-on-debian-ubuntu-linux/


Config Prometheus Target : /prometheus/prometheus.yml


==== Grafana Config :


sudo apt-get install -y apt-transport-https

sudo apt-get install -y software-properties-common wget

wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -

echo "deb https://packages.grafana.com/oss/deb stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

sudo apt-get update

sudo apt-get install grafana

sudo systemctl daemon-reload

sudo systemctl start grafana-server

sudo systemctl status grafana-server







config GUI metrics :  /prometheus/metrics-monitoring.txt


==== / PROMETHEUS SERVER CONFIG











==== Research & Development

--- Prometheus Server :

Prometheus : http://<YOUR_IP>:9090/  

Metrics Node Exporter : http://<YOUR_IP>:9100/metrics

Grafana : http://<YOUR_IP>:3000/



--- Confluent Server :

Metrics Jmx Exporter Zookeeper : http://<YOUR_IP>:8181/

Metrics Jmx Exporter Kafka : http://<YOUR_IP>:8282/

Control Center : http://<YOUR_IP>:9021/



==== / Research & Development



# Regards,

# Eki Indradi