# How to build `AmazonReviewData_preprocess.java` and `AmazonMetaData_matching.java` without installing any IDE stuff

You still need to install a JDK. I have no idea if the following is the "appropriate" way to build all these, but I was at least make the code run.

## Build

0. Get all the required jar files, except for `guava-30-1.1-jre.jar` (Google Core Libraries for Java), are included in [Galago 3.5](https://sourceforge.net/projects/lemur/files/lemur/galago-3.5/galago-3.5-bin.tar.gz/download). Download `guava-30-1.1-jre.jar` from [here](https://mvnrepository.com/artifact/com.google.guava/guava/30.1.1-jre). Create a `lib` directory and put all the jar files into it.

1. javac -cp lib/commons-lang-2.5.jar:lib/core-3.5.jar:lib/tupleflow-3.5.jar:lib/xz-1.0.jar:lib/json-20090211.jar:. -d . DataProcess.java 

2. javac -cp lib/commons-lang-2.5.jar:lib/core-3.5.jar:lib/tupleflow-3.5.jar:lib/xz-1.0.jar:lib/json-20090211.jar:. -d . AmazonReviewData_preprocess.java

3. javac -cp lib/commons-lang-2.5.jar:lib/core-3.5.jar:lib/tupleflow-3.5.jar:lib/xz-1.0.jar:lib/json-20090211.jar:lib/guava-30.1.1-jre.jar:. -d . AmazonMetaData_matching.java --add-exports jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED -Xlint:unchecked

## Run

1. java -cp lib/commons-lang-2.5.jar:lib/core-3.5.jar:lib/tupleflow-3.5.jar:lib/xz-1.0.jar:lib/json-20090211.jar:. edu.umass.ciir.hack.TextProcess.AmazonReviewData_preprocess ../example_jsonConfigFile.json Cell_Phones_and_Accessories_5.json.gz Cell_Phones_and_Accessories_5_processed.json.gz

2. java -cp lib/commons-lang-2.5.jar:lib/core-3.5.jar:lib/tupleflow-3.5.jar:lib/xz-1.0.jar:lib/json-20090211.jar:lib/guava-30.1.1-jre.jar:. --add-exports jdk.compiler/com.sun.tools.javac.util=ALL-UNNAMED edu.umass.ciir.hack.TextProcess.AmazonMetaData_matching ../example_jsonConfigFile.json meta_Cell_Phones_and_Accessories.json.gz indexmin_count5/
