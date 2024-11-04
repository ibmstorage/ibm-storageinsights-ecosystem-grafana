# ibm-storageinsights-ecosystem-grafana Setup Documentation

**As an open-source project, the IBM Storage Insights Grafana dashboard follows a community-supported model, so IBM does not provide formal support for this dashboard. Designed as a do-it-yourself solution, it allows users to customize and troubleshoot independently. However, if you encounter issues or have ideas for improvements, you can connect with the project’s contributors and submit your requests via the this GitHub page**

> **Note:** All steps outlined below must be performed by an **Admin User** to ensure proper permissions for setup and configuration.

## 1. Pre-requisites

### 1.1 Install Grafana
Ensure Grafana is installed with version 11.1.0 or later. If not, please refer to the document below for installation instructions.
- [Grafana Installation Guide](https://grafana.com/docs/grafana/latest/setup-grafana/installation/)

### 1.2 Install Plugins
1. **Infinity**: Required for custom data source integrations.
2. **Business Variables**: For dynamic variable creation and management.
3. **Text**: For adding textual content to dashboards.

Follow the link below for the procedure to browse & install the plugins:
- [Browse and Install Plugins Guide](https://grafana.com/docs/grafana/latest/administration/plugin-management/#browse-plugins)

### 1.3 Fetch the API key as an Admin User from Storage Insights
Follow the link below for the procedure to fetch the API key:
- [How to get API key from IBM SI](https://www.ibm.com/docs/en/storage-insights?topic=configuring-user-access-management#rest_api__section_dyd_t1t_jzb__title__1)

---

## 2. Creating Data Source

### 2.1 Setup Using Infinity Plugin
1. Navigate to **Menu > Connections > Data Sources**.
2. Click **Add new data source** button on the right-hand side top of the screen.
3. Enter **Infinity** in the search bar.
4. In the Settings Page, enter the name of the data source. (Example: `Fetch-Data-Tenant1`)
5. In the left-hand menu, select **Authentication**.
6. Select the authentication type as **API Key Value Pair**.
7. Enter the text **x-api-key** in the **Key** field.
8. Enter the API Key fetched from Storage Insights in the **Value** field.
9. Enter the text **https://insights.ibm.com** in the **Allowed Hosts** field and click on **Add** button.
10. Click on the **Save & Test** button.

---

## 3. Import Grafana Dashboard

### 3.1 Dashboard Import
1. Navigate to **Menu > Dashboard > Click on New Button > Import**.
2. Upload or paste the JSON file for the pre-configured dashboard.
3. Select the data source created as per step 2.
4. Once the dashboard is launched, enter the **SI Tenant ID** in the **TenantID** text box.
      (`Tenant ID info can be found from the SI UI URL. If your SI URL is https://insights.ibm.com/gui/XXXX-XXX-XXX-XXX, then TenantID is XXXX-XXX-XXX-XXX`)
6. Click on the **Save Dashboard** button.
7. Enable **"Save current variable values as dashboard default"**, this enables you to save the **TenantID** in the dashboard.
8. Click on **Save**.

---

## 4. Customizations
- Customize and configure the dashboard as needed to display the desired metrics and data from IBM Storage Insights.
