<project name="IIB-CI-MAIN" default="init" basedir="..">
  <description>IIB Continuous Integration Demo (main script)</description>

  <target name="init">
    <tstamp />
    <property environment="env" />
    <property name="path.build" value="Build" />
    <property name="path.tools" value="C:\Program Files\IBM\ACE\11.0.0.4\tools" />
    <property name="path.ace" value="C:\Program Files\IBM\ACE\11.0.0.4\server\bin" />
    <property name="base.dir" value="." />
    <property name="broker.file" value="${path.build}/brokerFile.txt" />
    <property name="ace.svr" value="default" />
    <antcall target="HTTPEchoApp" />
  </target>
  <target name="HTTPEchoApp">
    <!-- build workspace and create BAR file -->
    <echo message="Creating Bar"/>
    <property name="ace.bar" value="HTTPEchoApp.bar"/>
       <exec executable="${path.tools}/mqsicreatebar">
      <arg value="-data" />
      <arg value="${base.dir}" />
      <arg value="-b" />
      <arg value="${ace.bar}" />
      <arg value="-a" />
      <arg value="HTTPEchoApp" />
    </exec>
    <echo message="Deploying Bar"/>
    <exec dir="${path.build}" executable="Deploy.bat">
      <arg value="../${broker.file}" />
      <arg value ="${ace.svr}" />
      <arg value="../${ace.bar}" />
    </exec>
    <echo message="Deployement successful" />
  </target>
</project>

