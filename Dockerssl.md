Docker file:--

FROM ibmcom/ace
USER aceuser
COPY TestApplication.bar /home/aceuser/initial-config/bars/
COPY truststore.jks /home/aceuser/initial-config/truststore.jks
#COPY cert.arm /home/aceuser/initial-config/truststore/
COPY keystore.jks /home/aceuser/initial-config/keystore.jks
COPY odbc.ini /home/aceuser/initial-config/odbcini/
COPY setdbparms.txt /home/aceuser/initial-config/setdbparms/
#COPY initial-config/policy/* /home/aceuser/initial-config/policy/
COPY server.conf.yaml /home/aceuser/ace-server/server.conf.yaml
ENV ODBCINI /home/aceuser/initial-config/odbcini/odbc.ini
ENV ODBCSYSINI /home/aceuser/initial-config/odbcini/
WORKDIR /home/aceuser
USER root
RUN chown -R aceuser:mqbrkrs $ODBCINI && chmod 755 $ODBCINI
USER aceuser


Server.conf.yaml:-


---
ResourceManagers:
  JVM:
    truststoreType: 'JKS'
    truststoreFile: '/home/aceuser/initial-config/truststore.jks'
    truststorePass: 'brokertruststore::password'
    keystoreType: 'JKS'
    keystoreFile: '/home/aceuser/initial-config/keystore.jks'
    keystorePass: 'brokerkeystore::password'
    
# Defaults:
#   Policies:
#     HTTPSConnector: 'HTTPS'

Defaults:
 defaultApplication: ''       # Name a default application under which independent resources will be placed
 policyProject: 'DefaultPolicies'   # Name of the Policy project that will be used for unqualified Policy references
 Policies:
   # Set default policy names, optionally qualified with a policy project as {policy project}:name
   HTTPSConnector: 'HTTPS'          # Default HTTPS connector policy




setdbparms:----

# resource user password
#setdbparms::truststore "my username" truststorepwd
mqsisetdbparms -w /home/aceuser/ace-server -n LOKESHSOURCE -u LOKESH -p sarasu10
brokerkeystore::password ignore sarasu10
brokertruststore::password ignore sarasu10



odbc.ini


;#######################################
;#### List of data sources stanza ######
;#######################################

[ODBC Data Sources]
ORACLEDB=DataDirect ODBC Oracle Wire Protocol

;###########################################
;###### Individual data source stanzas #####
;###########################################

;# Oracle stanza
[LOKESHSOURCE]
Driver=/opt/ibm/ace-11/server/ODBC/drivers/lib/UKora95.so
Description=DataDirect ODBC Oracle Wire Protocol
HostName=192.168.2.251
PortNumber=1521
ServiceName=xe
CatalogOptions=0
EnableStaticCursorsForLongData=0
ApplicationUsingThreads=1
EnableDescribeParam=1
OptimizePrepare=1
WorkArounds=536870912
ProcedureRetResults=1
ColumnSizeAsCharacter=1
LoginTimeout=0
EnableNcharSupport=0
;# Uncomment the next setting if you wish to use Oracle TIMESTAMP WITH TIMEZONE columns
;# EnableTimestampwithTimezone=1

;##########################################
;###### Mandatory information stanza ######
;##########################################

[ODBC]
InstallDir=/opt/ibm/ace-11/server/ODBC/drivers
UseCursorLib=0
IANAAppCodePage=4
UNICODE=UTF-8

