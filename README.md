# Middleware gRPC
## Questions
#### What is gRPC and why does it work across languages and platforms?
gRPC is a Framework for RPC (Remote Procedure Calls) using HTTP and Protocol Buffers.  
It works across multiple languages and Platforms APIs for different languages are offered.

#### Describe the RPC life cycle starting with the RPC client?  
The client initiates an RPC call and sends it over HTTP to the Server.  
The Server processes the request and sends back a response which the client can then process

#### Describe the workflow of Protocol Buffers?  
Messages and services need to be defined in a .proto file which is compiled into language specific code.

#### What are the benefits of using protocol buffers?  
Protocol buffers are language and platform neutral and support forward, as well as backwards compatibility.  
The server and client can also be implemented in different languages

#### When is the use of protocol not recommended?
They are not recommended when a human-readable data format is required.  
The also shouldnt be used for small programs where they can cause unnecessary overhead.

#### List 3 different data types that can be used with protocol buffers?  
 * int32 (32 bit integer)
 * bool
 * string

## Protocol

To get the "Hello World" application in the E-Learning course up and running following Steps are required.

1) Create a new Gradle Project using IntelliJ
2) Download the src files from the course and unzip them into the project directory.
3) Remove the ".kts" file endings from "build.gradle.kts" and "settings.gradle.kts"
4) Replace the content of "build.gradle" with the following
```
plugins {
    id 'java'
    id 'com.google.protobuf' version '0.9.4' //to add
}

repositories {
    mavenCentral()
}

dependencies {
    implementation 'io.grpc:grpc-netty:1.68.1' //to add
    implementation 'io.grpc:grpc-protobuf:1.68.1' //to add
    implementation 'io.grpc:grpc-stub:1.68.1' //to add
    implementation 'io.grpc:grpc-api:1.68.1' //to add
    compileOnly 'javax.annotation:javax.annotation-api:1.3.2' //to add
}

//to add
protobuf {
    protoc {
        artifact = "com.google.protobuf:protoc:3.25.5"
    }
    plugins {
        grpc {
            artifact = 'io.grpc:protoc-gen-grpc-java:1.68.1'
        }
    }
    generateProtoTasks {
        all().each { task ->
            task.plugins {
                grpc {}
            }
        }
    }
}

sourceSets {
    main {
        java {
            srcDir 'build/generated/source/proto/main/java'
            srcDir 'build/generated/source/proto/main/grpc'
        }
    }
}
```
5) Now execute "gradle build"

Wait for gradle to finish building and the Project is set up.
You now have to set a valid JDK and are ready to use the Program.

You can execute "HelloWorldServer" to start the Server.  
Set a name in the code of "HelloWorldClient" and execute it.   
You should now see the name you set in the Terminal where the Server is running.