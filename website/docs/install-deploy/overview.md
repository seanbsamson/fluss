---
sidebar_label: "Overview"
title: Installation & Deployment
sidebar_position: 1
---

# Overview

Below, we provide an overview of the key components of a Fluss cluster, outlining their core functionalities and implementations. We also introduce the different deployment methods available for Fluss.

## Overview and Reference Architecture

The figure below shows the building blocks of a Fluss cluster:

<img width="1200px" src={require('../assets/deployment_overview.png').default} />



When deploying Fluss, multiple options are available for each building block. These options are listed in the table below the figure.


<table class="table table-bordered">
  <thead>
    <tr>
      <th class="text-left" width="250">Component</th>
      <th class="text-left" width="600">Purpose</th>
      <th class="text-left" width="300">Implementations</th>
    </tr>
   </thead>
   <tbody>
        <tr>
            <td>Fluss Client</td>
            <td>
                <p>
                    The Fluss Client is the primary entry point for users to interact with a Fluss Cluster. It is responsible for managing and operating the cluster through functions such as:
                </p>
                <ul>
                    <li> Administrative operations: creating or deleting databases, tables, and related resources.</li>
                    <li>Table operations: writing, reading, and deleting data</li>
                </ul>
            </td>
            <td>
                <ul>
                    <li>[Flink Connector](engine-flink/getting-started.md)</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>CoordinatorServer</td>
            <td>
                <p>
                The CoordinatorServer is the central work-coordination component of Fluss. It is responsible for:
                </p>
                <ul>
                    <li>Managing TabletServers</li>
                    <li>Managing cluster metadata</li>
                    <li>Coordinating the entire cluster, such as performing data rebalancing and recovering data when TabletServers fail.</li>
                </ul>
            </td>
            <td rowspan="2">
                <ul>
                    <li>[Local Cluster](install-deploy/deploying-local-cluster.md)</li>
                    <li>[Distributed Cluster](install-deploy/deploying-distributed-cluster.md)</li>
                    <li>[Docker run / Docker compose](install-deploy/deploying-with-docker.md)</li>
                </ul>
            </td>
        </tr>
        <tr>
            <td>TabletServer</td>
            <td>
                <p>
                TabletServers are the nodes responsible for managing and storing data.
                </p>
            </td>
        </tr>
        <tr>
            <td colspan="3" style={{ textAlign: "center" }}>
                <b>External Components</b>
            </td>
        </tr>
            <tr>
                <td>ZooKeeper</td>
                    <td>
                        :::warning
                        ZooKeeper will be removed in the near future to simplify deployment. For more details, please check out [Roadmap](/roadmap/).
                        :::
                        <p>
                        Fluss leverages ZooKeeper for distributed coordination across all running CoordinatorServer instances and for managing cluster metadata.
                        </p>
                    </td>
                    <td>
                        <ul>
                            <li><a href="https://zookeeper.apache.org/">ZooKeeper</a></li>
                        </ul>
                    </td>
                </tr>
            <tr>
            <td>Remote Storage (optional)</td>
            <td>
                Fluss uses file systems as remote storage to store snapshots for Primary-Key Tables and to store tiered log segments for Log Tables.
            </td>
            <td>
            <li>[HDFS](maintenance/filesystems/hdfs.md)</li>
            <li>[Aliyun OSS](maintenance/filesystems/oss.md)</li>
            <li>[Amazon S3](maintenance/filesystems/s3.md)</li>
            </td>
        </tr>
        <tr>
            <td>Lakehouse Storage (optional)</td>
            <td>
               Fluss’s DataLake Tiering Service continuously compacts Fluss’s Arrow files into Parquet/ORC files in an open lake format. Data stored in the Lakehouse layer can be read by Fluss clients using Union Read, and can also be accessed directly by query engines such as Flink, Spark, StarRocks, and Trino.
            </td>
            <td>
                <li>[Paimon](streaming-lakehouse/integrate-data-lakes/paimon.md)</li>
                <li>[Iceberg](streaming-lakehouse/integrate-data-lakes/iceberg.md)</li>
                <li>[Lance](streaming-lakehouse/integrate-data-lakes/lance.md)</li>
            </td>
        </tr>
        <tr>
            <td>Metrics Storage (optional)</td>
            <td>
                CoordinatorServers and TabletServers report internal metrics, and Fluss clients (e.g., connectors in Flink jobs) can also report additional client-specific metrics.
            </td>
            <td>
               <li>[JMX](maintenance/observability/metric-reporters.md#jmx)</li>
               <li>[Prometheus](maintenance/observability/metric-reporters.md#prometheus)</li>
            </td>
        </tr>
    </tbody>
</table>

## How to deploy Fluss

Fluss can be deployed in three different ways:
- [Local Cluster](install-deploy/deploying-local-cluster.md)
- [Distributed Cluster](install-deploy/deploying-distributed-cluster.md)
- [Docker run / Docker Compose](install-deploy/deploying-with-docker.md)

**NOTE**:
- Local Cluster is for testing purpose only.
