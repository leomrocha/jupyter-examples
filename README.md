# jupyter-examples

Jupyter examples with python, Bash, R and Scala kernels

## Introduction

This project is dedicated to be the materials for a private introduction training on installing Jupyter kernels
and working with 

These materials are public as they don't have any internal information. 

The actual presentation is not made public as it may contain sensitive information. Might be curated later made available but don't count on it.



## Notes

_Important:_ *jupyter* is the command name that replaced *ipython* command. If you are using an older version it might still be called *ipython*

The document Contains some notes that I made during the process of installing the  with more detailed instructions on what I did what worked and what didn't.

## Notebooks *.ipynb

This folder contain the notebooks that will be used during the presentation.

## Cassandra example data

For the Spark + Cassandra example, I've used the following keyspace, table and data creation:

  CREATE KEYSPACE test WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1 };
  CREATE TABLE test.kv(key text PRIMARY KEY, value int);
  --Then insert some example data:
  
  INSERT INTO test.kv(key, value) VALUES ('key1', 1);
  INSERT INTO test.kv(key, value) VALUES ('key2', 2);
  INSERT INTO test.kv(key, value) VALUES ('key3', 3);
  INSERT INTO test.kv(key, value) VALUES ('key4', 4);
  INSERT INTO test.kv(key, value) VALUES ('key5', 5);
  INSERT INTO test.kv(key, value) VALUES ('key6', 2);

