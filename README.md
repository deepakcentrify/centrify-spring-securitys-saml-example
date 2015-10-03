# Centrify Spring SAML Integration

### Overview
This document describes how to enable Centrify Identity Service (via SAML) to a Java Spring application which uses Spring Security SAML.   

This guide will provide step-by-step instruction on how to setup and run an example Centrify Spring SAML example 

### Requirements
1. Java 1.7+ SDK
2. Maven
3. Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files
    * Download the version that matches your installed JVM E.g. UnlimitedJCEPolicyJDK7.zip
    * Unzip the downloaded zip 
    * Copy local_policy.jar and US_export_policy.jar to the $JAVA_HOME/jre/lib/security (Note: these jars will be already there so you have to overwrite or back up them)


### Instructions
Step 0: Download centrify spring saml example project

    	   
	    git clone https://github.com/centrify/Centrify-Spring-SAML.git
	    
Step 1: Setup an Application using Custom SAML template in your Centrify Management Portal and download IDP matadata 
> In the folder /centrify, there is a zip file, which is the Spring SAML example Centrify APP, import it in your Centrify Management Portal. 

> If successfully imported, you can download this APP's metadata file, rename it as "centrify.idp.xml", put it in centrify folder (overwrite the previous one)

Step 2: run maven build command in the project root

        
        mvn clean install
        
>In this step, we have already configured the sample in src/main/webapp/WEB-INF/securityContext.xml. We configured that the IDP metadata will be obtained by classpath resource and we configured a SP with entityID "centrify.saml.test". 
>

Step 3: mvn tomcat:run-war-only
> In this step, the war file in step 2 will be deployed on a maven tomcat plugin

> If tomcat runs successfully, go to the [project entry] to check whether it runs well

Step 4: Obtain Service Provider (SP) metadata from Spring SAML example 
> If Step 3 works fine, go to "Metadata Administration", login as the default admin. You will see "centrify.saml.test" under "Service Providers".
>
> Click on "centrify.saml.test", and click "Download entity metadata" to save it as a file.

Step 5: Upload Service Provider (SP) metadata to Centrify Tenant
> Go back to your Centrify Tenant, in the SAML Application Settings, upload the SP metadata you have download in Step 4
>
> In Advanced panel, setAudience('centrify.saml.test'); please be careful that the audience should be the same as entityID in the SP metadata. setRecipient('http://localhost:8080/centrify-spring-saml-sample/saml/SSO'); this recipient should be the same as Assertion Consumer Service URL

Step 6: Test Centrify SAML authentication
> Now go back to SAML login page, choose the IDP and click “Start single sign-on”.
If it is your first time login, you will be redirect to Centrify User Portal to authenticate, after that, you will be redirected back to spring-spring-saml-integration-sample webpage and the user information will be displayed

### Version
1.0.0-SNAPSHOT

   [spring security saml]: <https://github.com/spring-projects/spring-security-saml>
   [project entry]: <http://localhost:8080/centrify-spring-saml-sample>
