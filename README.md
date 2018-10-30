# datagen

Thanks to @anarasimham for the python skeleton that was modifed for this data generator. 

### Here is the original data generation script:
https://github.com/anarasimham/data-gen

### Overview

The data generater uses the faker python library to generate random values for each attribute in a given schema. The ouput of the script is json format. In the script there are 5 unique data generators:

- CustomerDataGenerator
- SalesRepDataGenerator
- POSDataGenerator
- POSCustomerDataGenerator
- ManufacturingDataGenerator

The generated defaulted in the script is the POSDataGenerator.This can be modifed by changed the selected class used for generating the data. 

To modifiy what data generator is used, modifiy the d variable in the below code snippet in the python code. 
```python
if __name__ == '__main__':
    d = POSDataGenerator()
    for i in range(1,20000):
        record = d.gen_row()
        record = json.dumps(record)
        producer.send(KAFKA_TOPIC, record)
        print(record)
```




A kafka producer has been included as well as a sleep timer that will regulate the data generation. It is defaulted to 1 json record per second but this can be adjusted as required. 

```python
if __name__ == '__main__':
    d = POSDataGenerator()
    for i in range(1,20000):
        record = d.gen_row()
        record = json.dumps(record)
        producer.send(KAFKA_TOPIC, record)
        print(record)
```



### Python Library Requirements (use pip to install dependencies):
random, json, time, datetime, faker kafka

### Running the Script:

#### To run the script in the backgroud:
nohup python data-generator-kafka-producer.py &

#### To run the script and print to terminal:
python data-generator-kafka-producer.py
