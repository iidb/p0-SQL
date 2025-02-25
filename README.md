# The SQL Experiment

## Install sqlite3

### Linux

```shell
# Arch
sudo pacman -S --needed sqlite3
# Debian
sudo apt install sqlite3
```

### MacOS

`sqlite3` has been preinstalled.

### Windows

Download `sqlite-tools-win` in <https://www.sqlite.org/download.html>, and then add environment variables to the system.

## Import dataset (2pts)

We use the dataset in TPC-H in this experiment: the csv files under `data/`. This repo includes the specification of TPC-H: `tpc-h_v3.0.0.pdf`. Page 13 includes the schema of each table.

We have provided the SQL statements to create tables: `schema.sql`. You may create tables on Linux and Mac in this way:

```bash
sqlite3 test.db < schema.sql
```

Then you should import the dataset into the database. The statements should be saved in `load.sql`.

## Single table queries (5*1pts)

Save the SQL statements of the following queries in `<number>.sql`, such as `1.sql`, `2.sql`, etc. For some queries, we list the tables needed by the query in the brackets at the beginning of the query description.

Please note the order of the queries. An earlier query may affect a later query.

1. (`ORDERS`) Get the sum of `O_TOTALPRICE` of each customer with >20 orders. Each result row should include `O_CUSTKEY`, the sum of `O_TOTALPRICE`, and the number of orders.
2. (`LINEITEM`) Increase the tax on items with a discount >0.02 by 10%.
3. (`LINEITEM`) For each order, get the average discount of items with taxes <0.05. The results should be ordered by the average discount from largest to smallest. Only show the top 10 orders. Each result row should include `L_ORDERKEY` and the average discount.
4. (`LINEITEM`) Get the items with the largest discount. Each result row should include `L_ORDERKEY` and `L_LINENUMBER`.
5. (`PARTSUPP`) Get the sum of `PS_AVAILQTY` of each `PS_PARTKEY`. Each result row should include `PS_PARTKEY` and the sum of `PS_AVAILQTY`.

## Multi-table queries (3*1pts)

6. (`CUSTOMER`, `ORDERS`, `NATION`) Get the total price of all orders whose customers are from `CHINA`.

7. (`CUSTOMER`, `ORDERS`) Find all customers with at least one order whose total price <10000. Each result row should include all columns in `CUSTOMER`.

8. Find suppliers with >100 unique customers. Each result row should include the name of the supplier and the number of unique customers. The results should be firstly ordered by the number of unique customers from largest to smallest then ordered by the name of the supplier in descending order.

## Local test

```shell
make test
```

You may also test problems one by one:

```shell
python3 test.py load
python3 test.py 1
python3 test.py 2
python3 test.py 3
...
```

## Submit

```shell
make submit
```

Then submit `submission.zip` to autolab.

For Windows users:

1. The autograder runs on Linux whose path separator is `/`. Therefore, Windows users should replace the path separator `\` in `load.sql` with `/` before submitting.
2. `zip` command is not available on Windows by default. Therefore, Windows users need to pack `.sql` files into `submission.zip` manually.

If you have any questions, you may ask them in the WeChat group or Web Learning (aka 网络学堂).

## Links you may find useqful

<https://www.runoob.com/sqlite/sqlite-tutorial.html>

[How to import a csv file whose columns are separated by semicolons](https://sqlite.org/forum/forumpost/6b41812741)
