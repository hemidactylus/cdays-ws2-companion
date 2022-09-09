# Cassandra Days Workshop2 Companion

_Data Modeling + App Development_

![Banner](images/cd_banner.png)

## Steps

### Data Modeling part

Visualize the sensor-network data model example
in the Web-based tool KDM:

1. download the model definition file from [here](https://raw.githubusercontent.com/datastaxdevs/workshop-cassandra-data-modeling/main/materials/kdm_sensor_data.xml)
2. click [here](http://kdm.kashliev.com/) to open KDM and "File / Import project..." to use the file you just downloaded.
3. The entity-relationship diagram and the access patterns are filled for you.

### App development

_Note: the instructions here come from the following source repo, which you are encouraged to checkout for more: [Application Development Workshop](https://github.com/datastaxdevs/workshop-cassandra-application-development#readme)._

Create an [Astra DB instance](https://astra.datastax.com) if you haven't yet, with database=`workshops` and keyspace=`sensor_data`.
Get a secure-connect-bundle for your database.

Once your database is active,
locate the CQL console and paste the
contents of [this initialization script](https://raw.githubusercontent.com/datastaxdevs/workshop-cassandra-application-development/main/initialize.cql)
(which creates and populates the required tables).

Here are some queries to run in the CQL
console to test your data model:
```
-- Q1 (note 'all' is the only partition key in this table)
SELECT  name, description, region, num_sensors
FROM    networks
WHERE   bucket = 'all';

-- Q2
SELECT  date_hour, avg_temperature, latitude, longitude, sensor 
FROM    temperatures_by_network
WHERE   network    = 'forest-net'
  AND   week       = '2020-07-05'
  AND   date_hour >= '2020-07-05'
  AND   date_hour  < '2020-07-07';

-- Q3
SELECT * 
FROM    sensors_by_network
WHERE   network = 'forest-net';

-- Q4
SELECT  timestamp, value 
FROM    temperatures_by_sensor
WHERE   sensor = 's1003'
  AND   date   = '2020-07-06';
```

Finally, click on [this link](https://gitpod.io/#https://github.com/datastaxdevs/workshop-cassandra-application-development) (preferrably _open in new tab_)
and get ready to launch your API!

#### Homework and badges

Follow [these instructions](https://github.com/datastaxdevs/workshop-cassandra-application-development#homework-instructions) to complete
your lab assignment and get a nice verified "App Development with Cassandra" badge!

## Additional references

### Data Modeling part

Go to [datastax.com/learn/data-modeling-by-example](https://www.datastax.com/learn/data-modeling-by-example) for illustrative examples
of data modeling with Cassandra. Each comes with an interactive hands-on lab for practice!

For a more in-depth workshop on data modeling in Cassandra, visit this repo: [github.com/datastaxdevs/workshop-cassandra-data-modeling](https://github.com/datastaxdevs/workshop-cassandra-data-modeling).

### App Development part

Reference repository: [github.com/datastaxdevs/workshop-cassandra-application-development](https://github.com/datastaxdevs/workshop-cassandra-application-development#readme).
