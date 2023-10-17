# Problem Labels for Custom Apps-Logs

## Introduction

In this lab, you'll learn best practices for proactively monitoring custom applications. You'll learn how to create custom problem labels, new fields (EFDs, query time).

Estimated Lab Time: 15 minutes


### Objectives

In this lab, you will:
* Extract new fields using eval, extract
* Create new labels & EFDs from log-explorer
* Create new labels, EFDs in a Log Source
* Create alarms on new labels and verify

## **Task 1:**  Navigate to Sources

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
   ![](./images/admin-access.png "UIdescription")

2. Click on the option **Sources** inside **Resources** sidebar menu at the left.
   ![](./images/sources-access.png "UIdescription")

  Now you are in **Sources**.
   ![](./images/sources-page.png "UIdescription")

## **Task 2:**  Create User Defined Source

1. Click on **Create Source**.
   ![](./images/source-create-button.png "UIdescription")

2. Specify the **Name** and **Description (optional)**. Select **File** as **Source Type**. Select **Apache HTTP Server** at **Entity Types**.
   ![](./images/source-create-01.png "UIdescription")

3. Mark the **Specific parser(s)** option. Then, select **Apache HTTP Access Log Format**.
   ![](./images/source-create-02.png "UIdescription")

## **Task 3:**  Add Extended Fields

1. Click on **Extended Fields** and on **Add**.
   ![](./images/efd-create-01.png "UIdescription")

2. Select **Original Log Content** as **Base Field**.  
  Download sample logs file for [Log Sample](./files/log-sample.log)</br>
  Set the Log Sample at **Example Base Field Content**.  
  For **Extract Expression** set **source ip:?\s{Source IP:[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}}**.
   ![](./images/efd-create-02.png "UIdescription")

3. Click on **Test Definition** and see more details about test results.
   ![](./images/efd-create-03.png "UIdescription")

4. Click on **Add**.
   ![](./images/efd-create-04.png "UIdescription")

5. The extended field definition is added successfully.
   ![](./images/efd-create-05.png "UIdescription")

## **Task 4:**  Add Labels

1. Click on **Labels** and on **Add conditional label**.
   ![](./images/labels-create-01.png "UIdescription")

2. Select **Original Log Content** as **Input Field** and **Contains** as **Operator**. Add **source ip** and **Request blocked** in **Condition Value**.
   ![](./images/labels-create-02.png "UIdescription")

3. Click on **Create Label**.
   ![](./images/labels-create-03.png "UIdescription")

4. Specify a **Label** and **Description (optional)**. Mark the **Use this label to indicate a problem** checkbox inside **Denotes Problem**. Then, select **High** for **Problem Priority**. Click on **Create**.
   ![](./images/labels-create-04.png "UIdescription")

  The label is created successfully.
   ![](./images/labels-create-05.png "UIdescription")

5. Click on **Add**.
   ![](./images/labels-create-06.png "UIdescription")
   
  The conditional label is added successfully.
   ![](./images/labels-create-07.png "UIdescription")

## **Task 5:**  Save User Defined Source

1. Click on **Create Source**.
   ![](./images/source-create-03.png "UIdescription")
   
  The source is created successfully.
   ![](./images/source-create-04.png "UIdescription")

## **Task 6:**  Navigate to Log Explorer

1. Click on the **Log Explorer** option inside the drop-down menu.
   ![](./images/log-explorer-access.png "UIdescription")

2. Now you are in **Log Explorer**.
   ![](./images/log-explorer.png "UIdescription")

## **Task 7:**  Create a new Log Search

1. Type the following query in the text input: **'Entity Type' = 'Host (Windows)' and 'Log Source' = 'Windows System Events' | timestats count as logrecords by 'Log Source'**
   ![](./images/log-search-query.png "UIdescription")

2. Click on **Run** and see the results below.
   ![](./images/query-results.png "UIdescription")

## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oct 17 2023
