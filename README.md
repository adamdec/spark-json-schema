# spark-json-schema

This goal of the spark-json-schema library is to support input data integrity when loading json data into Apache Spark.
For this purpose, the library is able to read a given json-schema as input and generates a Spark representation of this schema, which can be used during loading json-files into Spark.
Without such a schema, Spark uses its built-in schema inference, which can be result in incomplete schema representations due to missing fields in the input data.
As a result, the spark-json-schema library allows to verify the input data before learning, which avoids the risk of faulty input data.

# Quickstart

Include the library under the following coordinates:

    libraryDependencies += "de.zalando.payana" % "spark-json-schema" % "0.1-SNAPSHOT"

Parse a given json-schema file by providing the path to the input file:
    
    val schema = SchemaConverter.convert("schemaFile.json")
    
Use the created schema when loading json-files into Spark:
    
    val json = sqlContext.read.schema(schema).json(source)
 
Files that are not according to the schema are marked as `null` and can be filtered out:
    
    todo...
 
After these steps you can be sure that all files that were loaded for further processing comply to your schema.


# Release
To build a new release there must be no uncommitted changes in the local git working copy.
Once this requirement is met you have to run the following command

	sbt release

In the process you will be asked for version numbers, but sensible default are provided.
In case the library has a dependency to an external "SNAPSHOT" version a confirmation is in required as otherwise the release wont be started.
