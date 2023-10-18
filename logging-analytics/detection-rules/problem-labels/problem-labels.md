# Problem Labels for Custom Apps-Logs

## Introduction

In this lab, you'll learn best practices for proactively monitoring custom applications. You'll learn how to create custom problem labels, new fields (EFDs, query time).

Estimated Lab Time: 20 minutes


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

2. Download sample logs file for [Log Sample](./files/log-sample.log)</br>
  Select **Original Log Content** as **Base Field**. Set the Log Sample for **Example Base Field Content**. For **Extract Expression** set **source ip:?\s{Source IP:[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}}**.
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

1. For this lab, we are going to save a query using **eval** command to add new fields for custom logs. In this case, we want to add a new field that counts the number of errors for each host name (server).   
  Type the following query in the text input: *** | eval err = 'Error ID' | stats count(err) as Errors by 'Host Name (Server)'**
   ![](./images/log-search-query.png "UIdescription")

3. Click on **Run** and see the results below.
   ![](./images/query-results.png "UIdescription")

## **Task 8:**  Save the Log Search

1. Click on **Save as...** option inside **Actions** drop-down menu.
   ![](./images/log-search-save-01.png "UIdescription")

2. Select a **Saved Search Compartment**. Specify the **Search Name** and the **Search Description (optional)**. Then, click on **Save** button.
   ![](./images/log-search-save-02.png "UIdescription")

  The log search is saved successfully.
   ![](./images/log-search-save-03.png "UIdescription")

## **Task 9:**  Navigate to Detection Rules

1. Click on the **Administration** option inside the drop-down menu to access to **Administration Overview**.
   ![](./images/admin-access.png "UIdescription")

2. Click on the option **Detection Rules** inside **Resources** sidebar menu at the left.
   ![](./images/detection-rules-access.png "UIdescription")

  Now you are in **Detection Rules**.
   ![](./images/detection-rules.png "UIdescription")

## **Task 10:**  Create Scheduled search detection rule

1. Click on **Create** inside **Detection Rules** page to start creating a new detection rule.
   ![](./images/detection-rules-create.png "UIdescription")

  We will create a **Scheduled search** type detection rule.
   ![](./images/scheduled-search-option.png "UIdescription")

2. Specify a **Rule name** and **Saved search compartment**. Then, select the **Saved search** we created for the scheduled task.
   ![](./images/scheduled-search-create-01.png "UIdescription")

3. Select **Monitoring** as **Target Service**. Specify a **Metric Compartment**, **Metric Namespace** and **Metric Name**. Finally, set the **Interval** to **1 Hours** and click on **Create detection rule**.
   ![](./images/scheduled-search-create-02.png "UIdescription")

  The detection rule is saved successfully.
   ![](./images/scheduled-search-create-03.png "UIdescription")

## **Task 11:**  Navigate to Alarm Definitions

1. Click on the navigation menu.
   ![](./images/alarms-create-01.png "UIdescription")

2. Click on **Observability and Management**. Then, click on **Alarm Definitions** inside **Monitoring**.
   ![](./images/alarms-create-02.png "UIdescription")

## **Task 12:**  Create Alarm

1. Click on **Create Alarm**.
   ![](./images/alarms-create-03.png "UIdescription")

2. Specify an **Alarm name** and select **Info** for **Alarm severity**. Specify an **Alarm body (optional)**.
   ![](./images/alarms-create-04.png "UIdescription")

3. Select a **Compartment**. Then, select the **Metric namespace** and **Metric name** we created for the **Detection Rules**. Set the **Interval** for **30 minutes**. Finally, select **Count** for **Statistic**.
   ![](./images/alarms-create-05.png "UIdescription")

4. Select the **Operator**, **Value** and **Trigger delay minutes**.
   ![](./images/alarms-create-06.png "UIdescription")

5. Click on **Create a topic**.
   ![](./images/alarms-create-07.png "UIdescription")

6. Specify a **Topic name** and **Topic description (optional)**. Select **Email** for **Suscription Protocol** and specify your email in **Subscription Email**. Click on **Create topic and subscription**.
   ![](./images/alarms-create-08.png "UIdescription")

7. Click on **Save alarm**.
   ![](./images/alarms-create-09.png "UIdescription")

  The alarm is saved successfully.
   ![](./images/alarms-create-10.png "UIdescription")

8. We should receive an email as result for the subscription.
   ![](./images/alarms-create-11.png "UIdescription")


## Acknowledgements
* **Author** - Oswaldo Osuna, Logging Analytics Development Team
* **Contributors** -  Kumar Varun, Logging Analytics Product Management - Kiran Palukuri, Logging Analytics Product Management - Vikram Reddy, Logging Analytics Development Team 
* **Last Updated By/Date** - Oct 18 2023
