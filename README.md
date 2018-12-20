# Security Analysis of Bitcoin Transactions through Statistical Graph Annotation

Money transaction using bitcoin is getting prevalent these days due to its government-free, secure, decentralized and open-sourced
design. It has been exploited for money laundering. However, it is still possible to detect some trail by analysing the structure of the transaction network. This project aims to construct a user transaction flow graph of bitcoins and analyze the security and networking properties. By developing basic heuristics, we bundled the public keys of the users from the transaction graph into the user bitcoin flow graph. In a case study of the Silk Road arrest, we demonstrated how coin-mixing trails could be discovered using the user flow graph.

## Introduction
This work consists of four steps. The first three steps are data preprocessing and the fourth step is visualization and graph analysis.
### 1. Blockchain data parsing
We parse the raw data in the bitcoin blockchain into transactions between public addresses as *tran.txt*. In *tran.txt*, each line represents one bitcoin transaction. The corresponding meanings of its columns:



| Column       | Corresponding meaning          | 
| ------------- |:-------------:|
| 1      | The public address of the sender | 
| 2      | The public address of the recepient     |  
| 3 | The value of the transaction      |  
| 4 | Data and time of the transaction      |  
| 5 | The block number of the transaction      |  



### 2. Linking related public addresses
We link the public addresses that are owned by the same user into *links.txt*, *along.txt*, *a2u.txt* and *u2a.txt*. 

Each line in *links.txt* is an undirected link between two public addresses. *along.txt* contains the addresses that are not linked to any other public addresses we have seen so far. Each line in *a2u.txt* is a *address:user_id* pair, mapping an public address to the id of its user. Each line in *u2a.txt* is a *user_id:addresses* pair, mapping an user id to the public addresses it owns, delimited by ','.

### 3. Creating the user graph 
We transform the transactions between public addresses in the step 1 into transactions between users and result in *user_graph.txt*. The corresponding meanings of its columns:

| Column       | Corresponding meaning          | 
| ------------- |:-------------:|
| 1      | The user id of the sender | 
| 2      | The user id of the recepient     |  
| 3 | Data and time of the transaction      |  
| 4 | The block number of the transaction      |  
| 5 | The value of the transaction      |  

The number of transactions between users will be less than the number of transactions between public addresses because multiple transactions between the same users at each timestamp are summed into one.

### 4. Graph analysis of the user graph
We include notebooks to demonstrate we graph analysis process. 



## Installation for step 1

Requirements:
1. Please make sure that you have the bitcoin blockchain in your computer, otherwise go to https://bitcoin.org/en/full-node#ubuntu-1604.
2. python packages: plyvel, python-bitcoinlib, and bitcoin-blockchain-parser (https://github.com/alecalve/python-bitcoin-blockchain-parser)


You can install the required python packages by running the following commands Unix in terminal: 

```
  cd blockchain-graph-analysis
  chmod +x ./pkg.sh
  ./pkgs.sh
```

## Instructions
For parsing, make sure you have the bitcoin blockchain ready in *blockchain_path*. You need to specify the date of the last blockchain you want to parse as *end_date*  and the directory for the parsing results as *out_dir* in *YYYY-MM-DD* format. 

Run in terminal:

```
python parsing.py blockchain_path end_date out_dir
```

For linking, you need to the parsed data ready and specify the directory of the results as *direc*. 

Run in terminal:

```
python linking.py direc
```

For creating the user graph, you need to the results from the previous steps and specify the directory of the results as *direc*. 

Run in terminal:

```
python ugraph.py direc
```

Once you get the user graph, you can use a variety of graph analysis methods.

The sample graph is in `sampleusergraph.txt`.

Graph analysis methods are outlined in `User Graph Analysis.ipynb`

## Report

**Report for this project can be seen [here](https://github.com/pranav-ust/bitcoin/blob/master/Security%20Analysis%20of%20Bitcoin%20Transactions%20through%0AStatistical%20Graph%20Annotation.pdf)**. Have a read on our analysis of some case studies and famous bitcoin frauds.