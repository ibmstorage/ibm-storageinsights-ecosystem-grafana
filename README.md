# ibm-storageinsights-ecosystem-grafana Setup Documentation

> **Note:** All steps outlined below must be performed by an **Admin User** to ensure proper permissions for setup and configuration.

## 1. Introduction to IBM Storage Insights and Grafana

[IBM Storage Insights](https://www.ibm.com/products/storage-insights) is an observability and AIOps platform for storage systems which helps administrators and SRE to monitor and manage their storage fleet.

IBM Storage Insights offers a suite of REST APIs that allow seamless integration of storage system data—such as configuration, performance, and health metrics—into a variety of external applications. These APIs support building an interconnected ecosystem where storage insights can enhance the functionality of operational dashboards, incident management systems, and even security platforms.

Many enterprise organizations rely on a variety of vendor-specific observability tools, yet Grafana stands out as the preferred solution for an integrated operations dashboard. Its flexibility and compatibility make it the ideal choice for creating a unified, single-pane view across multi-vendor environments. With the IBM Storage Insights REST APIs and a pre-configured Grafana dashboard template, customers can effortlessly integrate monitoring of IBM storage, switches, and servers into a Grafana-based operational dashboard.

This diagram below illustrates the integration of IBM Storage Insights with Grafana for monitoring storage systems in a user’s data center and a step-by-step explanation of the flow:

<img width="1120" alt="image" src="https://github.com/user-attachments/assets/817c5571-667f-472e-b811-4f348662024e">

1. **Fetch the REST API Key**:  
   - A user in the data center begins by fetching an API key from IBM Storage Insights, which is hosted on IBM Cloud. This API key is required to securely access data from Storage Insights.

2. **Configure API Key in Data Source**:  
   - The user configures the fetched API key in the Grafana data source settings, specifically in the **Infinity DataSource** plugin within Grafana. This setup allows Grafana to authenticate with IBM Storage Insights using the provided API key.

3. **Authenticate to Storage Insights**:  
   - Once configured, Grafana uses the API key to authenticate requests to IBM Storage Insights, allowing it to securely fetch storage-related data.

4. **Data Fetching in Grafana Dashboard**:  
   - Using the Infinity DataSource, Grafana periodically retrieves data from IBM Storage Insights. This data is then displayed on the Grafana dashboard, providing real-time monitoring and insights into the storage systems located in the user’s data center.

This setup enables users to view and analyze data from IBM Storage Insights directly within their Grafana dashboards, allowing for centralized monitoring of storage infrastructure across data centers.


## 2. Prerequisites for Grafana Integration


### 2.1 Install Grafana
Ensure Grafana is installed with version 11.1.0 or later. If not, please refer to the document below for installation instructions.
- [Grafana Installation Guide](https://grafana.com/docs/grafana/latest/setup-grafana/installation/)

### 2.2 Install Plugins
1. **Infinity**: Required for custom data source integrations.
2. **Business Variables**: For dynamic variable creation and management.
3. **Text**: For adding textual content to dashboards.

Follow the link below for the procedure to browse & install the plugins:
- [Browse and Install Plugins Guide](https://grafana.com/docs/grafana/latest/administration/plugin-management/#browse-plugins)

### 2.3 Fetch the API key as an Admin User from Storage Insights
Follow the link below for the procedure to fetch the API key:
- [How to get API key from IBM SI](https://www.ibm.com/docs/en/storage-insights?topic=configuring-user-access-management#rest_api__section_dyd_t1t_jzb__title__1)

---

## 3. Creating Data Source

### 3.1 Setup Using Infinity Plugin
1. Navigate to **Menu > Connections > Data Sources**.
2. Click **Add new data source** button on the right-hand side top of the screen.
3. Enter **Infinity** in the search bar.
4. In the Settings Page, enter the name of the data source. (Example: `Fetch-Data-Tenant1`)
5. In the left-hand menu, select **Authentication**.
6. Select the authentication type as **API Key Value Pair**.
7. Enter the text **x-api-key** in the **Key** field.
8. Enter the API Key fetched from Storage Insights in the **Value** field.
9. Enter the text **https://insights.ibm.com** in the **Allowed Hosts** field and click on **Add** button.
<img width="452" alt="image" src="https://github.com/user-attachments/assets/5ca97ad3-c60b-4aab-8875-277dcae73f29">

10. Click on the **Save & Test** button.

---

## 4. Import Grafana Dashboard

### 4.1 Dashboard Import
1. Navigate to **Menu > Dashboard > Click on New Button > Import**.
2. Upload or paste the JSON file for the pre-configured dashboard.
3. Select the data source created as per step 2.
4. Once the dashboard is launched, enter the **SI Tenant ID** in the **TenantID** text box. (Example: `01eb8cb2-d32d-1e60-88ae-c35e5b3b9751`)
5. Click on the **Save Dashboard** button.
<img width="452" alt="image" src="https://github.com/user-attachments/assets/741143bb-525a-423c-8175-03669feaff85">

6. Enable **"Save current variable values as dashboard default"**, this enables you to save the **TenantID** in the dashboard.
7. Click on **Save**.
<img width="452" alt="image" src="https://github.com/user-attachments/assets/c3f11bbc-efe2-4e7a-86c8-a9fcfc804d7c">

---

## 5. Customizations

To enhance your monitoring setup, you can create custom panels within the existing Grafana dashboard that are tailored to your specific requirements.

### 1. Building a New Panel

- **Select the Data Source**: Begin by choosing the Data Source configured for IBM Storage Insights.
- **Define the REST API URL**: Enter the specific API endpoint URL for the data you want to visualize.
- **Set up Secure Authentication**: In the request headers, ensure you include `x-api-token` as the key, with `${APIToken}` as the value for secure access.

### 2. Adding Parsing Options

- **Configure Parsing**: Based on the structure of your API response, adjust parsing options within the Data Source settings to correctly map and format incoming data.

### 3. Applying Transformations

- **Refine the Data**: Go to the **Transformation** tab to apply filters, aggregations, or reorganize your data as necessary to match the requirements of your custom panel.

For more details on specific APIs and parameters, refer to the **[IBM Storage Insights Swagger documentation](https://insights.ibm.com/restapi/docs/)**, which provides a comprehensive list of API endpoints and configurations.
