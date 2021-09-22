<project name="IIB-CI-MAIN" default="init" basedir="..">
<description>IIB Continuous Integration Demo (main script)</description>
<target name="init">
<tstamp />
<property environment="env" />
<property name="path.build" value="Build" />
<property name="path.tools" value="/opt/ace-11.0.0.7/tools" />
<property name="path.ace" value="/opt/ace-11.0.0.7/server/bin" />
<property name="base.dir" value="/root" />
<property name="path.store" value="/home/bandaru/Music" />
<antcall target="Application1" />
</target>
<target name="Application1">
<!-- build workspace and create BAR file -->
<echo message="Creating Bar"/>
<property name="ace.bar" value="${path.store}/Application1.bar"/>
<exec executable="${path.tools}/mqsicreatebar">
<arg value="-data" />
<arg value="${base.dir}" />
<arg value="-b" />
<arg value="${ace.bar}" />
<arg value="-a" />
<arg value="Application1" />
</exec>
</target>
</project>
