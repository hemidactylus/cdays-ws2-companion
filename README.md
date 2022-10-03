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

> Further references for you:
> [the sensor data model interactive example](https://www.datastax.com/learn/data-modeling-by-example/sensor-data-model),
> [a gallery of data-modeling interactive exercises](https://www.datastax.com/learn/data-modeling-by-example),
> [the full data-modeling workshop](https://github.com/datastaxdevs/workshop-cassandra-data-modeling#readme).

### App development

_Note: the instructions here come from the following source repo, which you are encouraged to check out for more: [Application Development Workshop](https://github.com/datastaxdevs/workshop-cassandra-application-development#readme)._
_**The only difference is that we automate the download of the secure-bundle using `astra-cli` and a few other steps. Read on for details**_

Create an [Astra DB instance](https://astra.datastax.com) if you haven't yet, with database=`workshops` and keyspace=`sensor_data` (please, stick to this keyspace name!).
You will be given a DB-specific Token while creating the DB: but since its permissions are not enough for us, **create a brand new DB-Administrator token**.
(_To do so, go to your main Astra DB dashboard and click on the "..." menu on the right of your database in the DB list, then choose "Generate Token"._)

#### Gitpod quick steps

Finally, click on [this link](https://gitpod.io/#https://github.com/datastaxdevs/workshop-cassandra-application-development) (preferrably _open in new tab_)
and get ready to launch your API! The next steps are just a barebones outline
(pay attention to your instructors)

- Authorize Gitpod single sign-on and wait for the Gitpod IDE to fully load
- `curl -Ls "https://dtsx.io/get-astra-cli" | bash` to install the Astra CLI
- `. ~/.bashrc ; astra setup` and enter your Astra token (`AstraCS:....`)
- (optional) `astra db list` and `astra db list-keyspaces workshops`, `astra db get workshops` to check your DB
- Create and populate tables: `astra db cqlsh workshops -f initialize.cql`
- (optional) Test previous step: open cqlsh with `astra db cqlsh workshops -k sensor_data` and then run the sample queries given below
- Download SCB: `astra db download-scb -f secure-connect-workshops.zip workshops` and then `ls *zip` to check
- `cp .env.sample .env ; gp open .env` and replace Client ID and Client Secret from your token

#### Sample queries

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
SELECT  *
FROM    sensors_by_network
WHERE   network = 'forest-net';

-- Q4
SELECT  timestamp, value 
FROM    temperatures_by_sensor
WHERE   sensor = 's1003'
  AND   date   = '2020-07-06';
```

#### Choose your path

Now pick your language and continue either with [Java](https://github.com/datastaxdevs/workshop-cassandra-application-development/blob/main/java/Java_README.md) or [Python](https://github.com/datastaxdevs/workshop-cassandra-application-development/blob/main/python/Python_README.md).

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
