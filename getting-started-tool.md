---

copyright:
  years: 2015, 2021
lastupdated: "2021-09-30"

subcollection: discovery

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:deprecated: .deprecated}
{: codeblock}: .codeblock}
{:screen: .screen}
{:download: .download}
{:hide-dashboard: .hide-dashboard}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:curl: .ph data-hd-programlang='curl'}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:ruby: .ph data-hd-programlang='ruby'}
{:swift: .ph data-hd-programlang='swift'}
{:go: .ph data-hd-programlang='go'}

# Getting started with Discovery
{: #getting-started}

In this short tutorial, we introduce the {{site.data.keyword.discoveryshort}} tooling and go through the process of creating a private data collection and searching it.
{: shortdesc}

If you prefer to work in the API, see [Getting started with the API](/docs/discovery?topic=discovery-gs-api).

This documentation applies to {{site.data.keyword.discoveryshort}} service instances that you create with a Lite or an Advanced plan, or that you created with a Premium plan before 16 July 2020. For more information about features in Premium plan instances created on or after 16 July 2020 and in Plus (including Plus Trial) plan instances, see [these docs](/docs/discovery-data?topic=discovery-data-getting-started){: external}.
{: important}

## Before you begin
{: #before-you-begin-tool}
{: hide-dashboard}

You need a service instance to start.

1.  Go to the [{{site.data.keyword.discoveryshort}}](https://{DomainName}/catalog/services/discovery){: external} page in the {{site.data.keyword.cloud_notm}} catalog.

    The service instance is created in the **default** resource group if you do not choose a different one, and it *cannot* be changed later. This group is sufficient for the purposes of trying out the service.

    If you are creating an instance for more robust use and need information about organizing resource groups, see [Best practices for organizing resources and assigning access](https://{DomainName}/docs/account?topic=account-account_setup){: external}.
1.  Sign up for a free {{site.data.keyword.cloud_notm}} account or log in.
1.  Click **Create**.

## Step 1: Launch the tooling
{: #launch-the-tooling}

After you create an instance of {{site.data.keyword.discoveryshort}}, you're taken to your list of services.

1.  Click the {{site.data.keyword.discoveryshort}} instance you created to go to the service dashboard.
1.  On the **Manage** page, click **Launch Watson Discovery**. If you're prompted to log in to the tooling, provide your {{site.data.keyword.cloud_notm}} credentials.

## Step 2: Create a collection
{: #create-a-collection-tool}

Your first step in the {{site.data.keyword.discoveryshort}} tooling is to create a data collection.

A collection is a set of your documents. *Why would I want more than one collection?* There are a few reasons:

- You might want multiple collections to separate results for different audiences.
- The data might be so different that it doesn't make sense for it all to be queried at the same time.

The public, pre-enriched {{site.data.keyword.discoverynewsshort}} data collection is also available for your use. It is ready to query, and you can begin to create queries on it immediately. You cannot adjust its configuration or add documents to {{site.data.keyword.discoverynewsshort}}.

1.  Click ![Environment details](images/env_icon.png)<!-- {width="20" height="20" style="padding-left:5px;padding-right:5px;"} --> and choose **Create environment**.
1.  When your environment is ready, click the **Upload your own data** button, then you can **Name your new collection**. Name your collection **InstallDocs**.

    When creating a collection, under **Advanced**, you have the option to choose a configuration file named **Default Contract Configuration**. This configuration supports only the Element Classification enrichment, which can be used to extract party, nature, and category from elements in PDFs. See [Element Classification](/docs/discovery?topic=discovery-element-classification#element-collection) for details. Do not choose this option for this tutorial.

    The Element Classification enrichment is deprecated and will no longer be available, effective **10 July 2020**.
    {: important}

You can also crawl Box, Salesforce, Microsoft SharePoint Online, IBM Cloud Object Storage, and Microsoft SharePoint 2016 data sources, or do a web crawl with the {{site.data.keyword.discoveryshort}} tooling. Click the **Connect a data source** button and see [Connecting to data sources](/docs/discovery?topic=discovery-sources) for more information.
{: tip}

If you have recently deleted a Lite instance and then receive a `400 - Only one free environment is allowed per resource group` error message when creating a new environment in a new Lite instance, you need to finish deleting the original Lite instance. See [ibmcloud resource reclamations](/docs/cli?topic=cli-ibmcloud_commands_resource#ibmcloud_resource_reclamations) and follow the `reclamation-delete` instructions.
{: important}

## Step 3: Download the sample document and upload to your collection
{: create-custom-configuration}

1.  Download this sample PDF document: <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/discovery/watsonexplorerinstall.pdf" download>Watson Explorer Installation Guide <img src="../icons/launch-glyph.svg" alt="External link icon" title="External link icon"></a>. See [Supported document types](/docs/discovery?topic=discovery-sdu#doctypes) for the full list of document types supported in {{site.data.keyword.discoveryshort}}. 

    In some browsers, the link opens in a new window instead of saving locally. If this occurs, select `Save As` in your browser's `File` menu to save a copy of the file.
    {: tip}

1.  Upload the document to your collection. Either drag and drop it into your collection, or click **browse from computer** to upload documents. After the upload is complete, the following information displays:
    -  The number of documents (1).
    -  The fields identified from your document. You should see one field identified, `text`. We identify additional fields in a bit.
    -  Enrichments applied to your document. The Entity Extraction, Sentiment Analysis, Category Classification, and Concept Tagging enrichments are automatically applied to the `text` field by {{site.data.keyword.discoveryshort}}. For more information about enrichments, see [Adding enrichments](/docs/discovery?topic=discovery-configservice#adding-enrichments). 
    -  Pre-built queries you can run immediately.
1.  Let's try a quick Natural Language Query to level set. Click **Build your own query** on the lower right.
1.  On the **Build queries** screen, click on **Search for documents**, then **Use natural language**. Enter `What are the minimum hardware requirements` and click the **Run query** button. Click the **JSON** tab on the right. The result is not as precise as it could be, so let's improve it with Smart Document Understanding.
1.  Click on the name of the collection (**InstallDocs**) on the upper left to return to the **Overview** screen.  
 
## Step 4: Annotate your document
{: #upload-your-documents}

For more information about annotating documents, see [Smart Document Understanding](/docs/discovery?topic=discovery-sdu).
{: tip}

1.  Click **Configure data** on the upper right. 
1.  On the **Configure data** screen, there are three tabs: **Identify fields**, **Manage fields**, and **Enrich fields**.
1.  The `Watson Explorer Installation Guide` is displayed and ready for annotation on the **Identify fields** tab. All available fields (`answer`, `author`, `footer`, `header`, `question`, `subtitle`, `table_of_contents`, `text`, and `title`) are displayed in the **Field labels** list on the right. If you purchase an Advanced or Premium plan you can create your own custom labels.

    Since the entire document is currently identified as `text`, the  markers on the right side are entirely in yellow. As you annotate (and the system starts predicting), the colors update.
    {: tip}

1.  Click on `title`, then select the marker next to `Installation and Integration Guide`. Click **Submit page**.
1.  In the page preview on the left, click on page 3. Note that the `title` is already predicted for this page. Click **Submit page**.
1.  On page 4, select the `footer` label and select the marker next to the footer. Click the **Submit page** button.
1.  On pages 5 and 6, annotate the footers with the `footer` label. Submit each page. Click through a few more pages; note that the footer was predicted properly by {{site.data.keyword.discoveryshort}}. Annotate the `title`s (flush left) and `subtitle`s (indented) on pages 7, 9, and 10 and submit each page individually.
1.  Click through a few more pages and check the predicted titles and subtitles. If any need to be changed, annotate those pages, and click **Submit page**.
1.  Now click on the **Manage fields** tab and under **Improve query results by splitting your documents** split the document, based on `subtitle`. 
1.  Click the **Apply changes to collection** button on the top right. An **Upload your documents** dialog box appears. Browse to the original `watsonexplorerinstall.pdf` file, and upload it. All of the annotations are applied to your index. After it finishes indexing, the **Overview** screen opens. Expect to now see more than 30 documents and 4 fields identified from your data: `footer`, `subtitle`, `text`, and `title`. If the changes do not display within a few minutes, refresh the browser window.

    You can exclude fields, such as `footer`, from being indexed by opening the **Manage fields** tab and toggling that field `off`.
    {: tip}

## Step 5: Let's query
{: #build-a-query}

1.  Click **Build your own query** on the bottom right.
1.  On the **Build queries** screen, click on **Search for documents**, then **Use natural language**. Enter `What are the minimum hardware requirements` and click the **Run query** button. 
1.  Click the **JSON** tab on the right. Look at the `text` under `results`. The answers returned for the query are much more precise.

Additional resources:
-  To learn more about the data schema of your documents, click the **View Data Schema** icon or click on the **JSON** tab. See the [Discovery data schema](/docs/discovery?topic=discovery-query-concepts#discovery-schema) for details.
-  Click the **Use a sample query** button to try out example queries written in the {{site.data.keyword.discoveryshort}} Query Language.

## Next steps
{: #next-steps-tool}

Now, you have a functioning and populated {{site.data.keyword.discoveryshort}} instance. You can now begin customizing your collection by adding more documents and enrichments, and annotating additional documents. See [Smart Document Understanding](/docs/discovery?topic=discovery-sdu) for more information.