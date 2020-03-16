# Pulse Util Tool

python script to create required mongodb sink connector properties file.

## Dependencies

* Inorder to run the script we need python 3.6.x 64 bit.
* All the required libraries are in requirements.txt

use `pip3 install -r requirements.txt` to install those for `Linux`.


use `pip install -r requirements.txt` to install those for `Windows`.

## Execution

### STEP 1
This script takes three arguments namely --s, --c, --i
```
    --s <mongodb connector filename's suffix and schema name>
    --c <mongodb collection name>
    --i <column name to include from structure.csv which will be used in SMT of the message>
```
To generate the mongodb properties file run

`python3 parseyaml.py --s <filename> --c <collection name> --i <column name>` **For linux**

`python parseyaml.py --s <filename> --c <collection name> --i <column name>` **For windows**

### STEP2
copy the generated mongodb sink connector properties file to confluent-5.4.x 's directory
usually 

`~/confluent-5.4.x/etc/kafka/`

### STEP3
To run the source and sink use 

`./bin/connect-standalone ./etc/kafka/<worker.properties> ./etc/kafka/<csv-source-connector.properties> ./etc/kafka/<generated mongodb sink properties>`

##### P.S create the collection in mongodb before executing step3







