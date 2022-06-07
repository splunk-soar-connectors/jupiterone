[comment]: # "Auto-generated SOAR connector documentation"
# JupiterOne

Publisher: JupiterOne Inc\.  
Connector Version: 1\.0\.1  
Product Vendor: JupiterOne Inc\.  
Product Name: JupiterOne  
Product Version Supported (regex): "\.\*"  
Minimum Product Version: 5\.2\.0  

This app integrates with JupiterOne to perform investigative actions

[comment]: # " File: README.md"
[comment]: # ""
[comment]: # "    Copyright (c) JupiterOne Inc., 2022"
[comment]: # ""
[comment]: # "    This unpublished material is proprietary to JupiterOne."
[comment]: # "    All rights reserved. The methods and"
[comment]: # "    techniques described herein are considered trade secrets"
[comment]: # "    and/or confidential. Reproduction or distribution, in whole"
[comment]: # "    or in part, is forbidden except by express written permission"
[comment]: # "    of JupiterOne."
[comment]: # ""
[comment]: # "    Licensed under the Apache License, Version 2.0 (the 'License');"
[comment]: # "    you may not use this file except in compliance with the License."
[comment]: # "    You may obtain a copy of the License at"
[comment]: # ""
[comment]: # "        http://www.apache.org/licenses/LICENSE-2.0"
[comment]: # ""
[comment]: # "    Unless required by applicable law or agreed to in writing, software distributed under"
[comment]: # "    the License is distributed on an 'AS IS' BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND,"
[comment]: # "    either express or implied. See the License for the specific language governing permissions"
[comment]: # "    and limitations under the License."
[comment]: # ""
It is recommended to read the documentation for the app to understand the functioning of the actions
and the asset configuration or the action parameters associated with it. For further details, refer
to [JupiterOne
Docs](https://support.jupiterone.io/hc/en-us/articles/360022722094-JupiterOne-Platform-API) .

## Port Details

The app uses HTTP/ HTTPS protocol for communicating with the JupiterOne server. Below are the
default ports used by the Splunk SOAR Connector.

| SERVICE NAME | TRANSPORT PROTOCOL | PORT |
|--------------|--------------------|------|
| http         | tcp                | 80   |
| https        | tcp                | 443  |

## Steps to Configure the JupiterOne Phantom app's asset

Follow these steps to create an asset for the app in Phantom Platform:

-   Log in to the JupiterOne platform.

      

    -   Once logged in, a search box is shown where you can ask a question, enter a query, or run a
        full-text search.
    -   Please enter the following query in the search box: FIND jupiterone_account as a return
        a.\_accountId and press Enter.
    -   Copy the \_accountId returned in output into any text editor.
    -   Click on **Settings** gear found at the top right corner and select **Account Parameters** .
    -   Select the **USER API KEYS** section by clicking on **Key** icon available at the left side
        bottom of the page and create an API key by providing **Key name** and **Days before
        expiration** .
    -   The API Key would be created and would be displayed in a dialog box.
    -   Copy the **Token** value from the dialog box and paste it into any text editor as backup, as
        it won't be visible again. Once copied, click on Done.
    -   This token value is the **API Key** that will be used in the asset.

-   Log in to your Phantom platform.

      

    -   Navigate to the **Home** dropdown and select **Apps** .
    -   Search the JupiterOne App from the search box.
    -   Click on the **CONFIGURE NEW ASSET** button.
    -   Navigate to the **Asset Info** tab and enter the Asset name and Asset description.
    -   Navigate to the **Asset Settings** tab.
    -   Paste the **API Key** that was created from the JupiterOne UI and **Account ID** that was
        fetched by hitting a J1QL query from JupiterOne to its respective configuration parameter.
    -   Save the asset.
    -   Now, test the connectivity of the Phantom server to the JupiterOne instance by clicking on
        the **TEST CONNECTIVITY** button.

## Explanation of the Asset Configuration Parameters

The asset configuration parameters affect 'test connectivity' and some other actions of the
application. The parameters related to test connectivity action are JupiterOne Account ID and API
Key.

-   **JupiterOne Account ID:** JupiterOne Account ID for asset authorization.
-   **API Key** : API Key for asset authorization.

## Explanation of the JupiterOne Actions' Parameters

-   ### Test Connectivity (Action Workflow Details)

    -   This action will test the connectivity of the Phantom server to the JupiterOne instance by
        making an initial API call to a minimal query using the provided asset configuration
        parameters.
    -   The action validates the provided asset configuration parameters. Based on the API call
        response, the appropriate success and failure message will be displayed when the action gets
        executed.

-   ### Run Query

    Fetch the results from the JupiterOne platform for the given J1QL(JupiterOne Query Language)
    query. The pagination is implemented internally in this action which will paginate through the
    responses. The max results parameter can be used to limit the output responses. The data paths
    of the action contain the paths of response data that the queries (used for testing) returned.

    -   **Action Parameter: Query**

          

        -   This parameter will accept the J1QL query for a JupiterOne platform. An error message
            will be shown if the J1QL query is invalid.

    -   **Action Parameter: Max Results**

          

        -   This parameter allows the user to limit the number of results. It expects a numeric
            value as an input. The default value is 250 for which it will fetch the first 250
            results for a particular query.

    -   **Action Parameter: Include Deleted**

          

        -   This parameter includes recently deleted information in the results, when set to true.

    -   **Examples:**
        -   Retrieve 10 results for the query 'find Record'.

            -   Query = "find Record"
            -   Max Results = 10
            -   Include Deleted = false

              
            **Note:** Max Results value will be handled internally, which will paginate through the
            results for a particular query.

        <!-- -->

        -   Retrieve the results for the query 'find Record'.

            -   Query = "find Record"
            -   Max Results = 250
            -   Include Deleted = false

              
            **Note:** Max Results value will be handled internally, which will paginate through the
            results for a particular query.

        <!-- -->

        -   Retrieve the results for the query 'find Record'. The results should include the deleted
            entities.

            -   Query = "find Record"
            -   Max Results = 250
            -   Include Deleted = true

              
            **Note:** Max Results value will be handled internally, which will paginate through the
            results for a particular query.


### Configuration Variables
The below configuration variables are required for this Connector to operate.  These variables are specified when configuring a JupiterOne asset in SOAR.

VARIABLE | REQUIRED | TYPE | DESCRIPTION
-------- | -------- | ---- | -----------
**account\_id** |  required  | string | JupiterOne Account ID
**api\_key** |  required  | password | API Key

### Supported Actions  
[test connectivity](#action-test-connectivity) - Validate the asset configuration for connectivity using supplied configuration parameters  
[run query](#action-run-query) - Run a search query  

## action: 'test connectivity'
Validate the asset configuration for connectivity using supplied configuration parameters

Type: **test**  
Read only: **True**

#### Action Parameters
No parameters are required for this action

#### Action Output
No Output  

## action: 'run query'
Run a search query

Type: **investigate**  
Read only: **True**

The <b>query </b> parameter accepts J1QL query \(eg\: find Record\) as well as the full\-text search\. The full\-text search query needs to enclosed in double\-quotes\(""\) \(eg\: "assets"\)\. Please refer <a href='https\://support\.jupiterone\.io/hc/en\-us/articles/360022720434\-J1QL\-Query\-Tutorial' target='\_blank'>JupiterOne Query Language Tutorial</a> for J1QL reference\. The <b>max\_results</b> parameter overwrites the LIMIT if mentioned in the J1QL\. \(For instance, if query parameter has value "find Record LIMIT 20" and max\_results parameter has value "10", the action would return 10 records\. This implementation was added because the LIMIT in query accept values only between 1 and 250\.\)\.

#### Action Parameters
PARAMETER | REQUIRED | DESCRIPTION | TYPE | CONTAINS
--------- | -------- | ----------- | ---- | --------
**query** |  required  | J1QL query to run | string |  `jupiterone query` 
**max\_results** |  optional  | Maximum number of results to fetch for the query\. The default value is 250 | numeric | 
**include\_deleted** |  optional  | Include recently deleted entities in query/search | boolean | 

#### Action Output
DATA PATH | TYPE | CONTAINS
--------- | ---- | --------
action\_result\.parameter\.query | string |  `jupiterone query` 
action\_result\.parameter\.max\_results | numeric | 
action\_result\.parameter\.include\_deleted | boolean | 
action\_result\.data\.\*\.id | string | 
action\_result\.data\.\*\.entity\.\_id | string | 
action\_result\.data\.\*\.entity\.\_key | string | 
action\_result\.data\.\*\.entity\.\_source | string | 
action\_result\.data\.\*\.entity\.\_beginOn | string | 
action\_result\.data\.\*\.entity\.\_deleted | boolean | 
action\_result\.data\.\*\.entity\.\_version | numeric | 
action\_result\.data\.\*\.entity\.\_accountId | string | 
action\_result\.data\.\*\.entity\.\_createdOn | string | 
action\_result\.data\.\*\.properties\.name | string | 
action\_result\.data\.\*\.properties\.DisplayName | string | 
action\_result\.data\.\*\.entity\.displayName | string | 
action\_result\.data\.\*\.entity\.\_integrationName | string | 
action\_result\.data\.\*\.entity\.\_integrationType | string | 
action\_result\.data\.\*\.entity\.\_integrationInstanceId | string | 
action\_result\.data\.\*\.entity\.\_integrationDefinitionId | string | 
action\_result\.data\.\*\.properties\.tag\.Production | boolean | 
action\_result\.data\.\*\.properties\.tag\.AccountName | string | 
action\_result\.data\.\*\.properties\.tags | string | 
action\_result\.data\.\*\.properties\.website | string | 
action\_result\.data\.\*\.properties\.emailDomain | string | 
action\_result\.data\.\*\.properties\.id | string | 
action\_result\.data\.\*\.properties\.accountId | string | 
action\_result\.data\.\*\.properties\.privacyPolicy | boolean | 
action\_result\.data\.\*\.properties\.accountFullName | string | 
action\_result\.data\.\*\.properties\.companyFullName | string | 
action\_result\.data\.\*\.properties\.companyOverview | string | 
action\_result\.data\.\*\.properties\.termsConditions | boolean | 
action\_result\.data\.\*\.properties\.companyShortName | string | 
action\_result\.data\.\*\.properties\.companyWebsiteURL | string | 
action\_result\.data\.\*\.properties\.accountCompanyRole | string | 
action\_result\.data\.\*\.properties\.companyEmailDomain | string | 
action\_result\.data\.\*\.properties\.onboardingComplete | boolean | 
action\_result\.data\.\*\.properties\.currentOnboardingStep | numeric | 
action\_result\.data\.\*\.properties\.iconWebLink | string | 
action\_result\.data\.\*\.entity\.\_scope | string | 
action\_result\.data\.\*\.properties\.type | string | 
action\_result\.data\.\*\.properties\.deleteProtected | boolean | 
action\_result\.data\.\*\.properties\.endpoints | string | 
action\_result\.data\.\*\.properties\.projectId | string | 
action\_result\.data\.\*\.properties\.dummy\_column | string | 
action\_result\.data\.\*\.properties\.column1 | numeric | 
action\_result\.data\.\*\.properties\.Test | string | 
action\_result\.data\.\*\.properties\.email | string | 
action\_result\.data\.\*\.properties\.active | boolean | 
action\_result\.data\.\*\.properties\.picture | string | 
action\_result\.data\.\*\.properties\.username | string | 
action\_result\.data\.\*\.properties\.createdOn | string | 
action\_result\.data\.\*\.properties\.givenName | string | 
action\_result\.data\.\*\.properties\.familyName | string | 
action\_result\.data\.\*\.properties\.mfaEnabled | boolean | 
action\_result\.data\.\*\.properties\.emailVerified | boolean | 
action\_result\.data\.\*\.properties\.instanceId | string | 
action\_result\.data\.\*\.properties\.state | string | 
action\_result\.data\.\*\.properties\.output | string | 
action\_result\.data\.\*\.properties\.severity | string | 
action\_result\.data\.\*\.properties\.plugin\.id | numeric | 
action\_result\.data\.\*\.properties\.port\.port | numeric | 
action\_result\.data\.\*\.properties\.scan\.uuid | string | 
action\_result\.data\.\*\.properties\.asset\.uuid | string | 
action\_result\.data\.\*\.properties\.lastSeenOn | string | 
action\_result\.data\.\*\.properties\.last\_found | string | 
action\_result\.data\.\*\.properties\.firstSeenOn | string | 
action\_result\.data\.\*\.properties\.first\_found | string | 
action\_result\.data\.\*\.properties\.severity\_id | numeric | 
action\_result\.data\.\*\.properties\.port\.protocol | string | 
action\_result\.data\.\*\.properties\.scan\.started\_at | string | 
action\_result\.data\.\*\.properties\.scan\.completed\_at | string | 
action\_result\.data\.\*\.properties\.severity\_default\_id | numeric | 
action\_result\.data\.\*\.properties\.severity\_modification\_type | string | 
action\_result\.data\.\*\.properties\.port\.service | string | 
action\_result\.data\.\*\.properties\.exception | boolean | 
action\_result\.data\.\*\.properties\.\@exception | string | 
action\_result\.data\.\*\.properties\.exceptionReason | string | 
action\_result\.data\.\*\.properties\.\@exceptionReason | string | 
action\_result\.data\.\*\.properties\.priority | string | 
action\_result\.data\.\*\.properties\.numericPriority | numeric | 
action\_result\.data\.\*\.properties\.updatedOn | string | 
action\_result\.data\.\*\.properties\.description | string | 
action\_result\.data\.\*\.properties\.uuid | string | 
action\_result\.data\.\*\.properties\.uuidId | string | 
action\_result\.data\.\*\.properties\.enabled | boolean | 
action\_result\.data\.\*\.properties\.userName | string | 
action\_result\.data\.\*\.properties\.permissions | numeric | 
action\_result\.data\.\*\.properties\.containerUuid | string | 
action\_result\.data\.\*\.properties\.loginFailCount | numeric | 
action\_result\.data\.\*\.properties\.loginFailTotal | numeric | 
action\_result\.data\.\*\.properties\.lastlogin | numeric | 
action\_result\.data\.\*\.properties\.\@dummy\_column | string | 
action\_result\.data\.\*\.properties\.impact | string | 
action\_result\.data\.\*\.properties\.category | string | 
action\_result\.data\.\*\.properties\.reporter | string | 
action\_result\.data\.\*\.properties\.reportable | boolean | 
action\_result\.data\.\*\.properties\.resolvedAt | string | 
action\_result\.data\.\*\.properties\.open | boolean | 
action\_result\.data\.\*\.properties\.level | string | 
action\_result\.data\.\*\.properties\.status | string | 
action\_result\.data\.\*\.properties\.webLink | string | 
action\_result\.data\.\*\.properties\.numericSeverity | numeric | 
action\_result\.data\.\*\.properties\.version | numeric | 
action\_result\.data\.\*\.properties\.specVersion | numeric | 
action\_result\.data\.\*\.properties\.column2 | numeric | 
action\_result\.data\.\*\.properties\.column3 | string | 
action\_result\.data\.\*\.properties\.column4 | numeric | 
action\_result\.data\.\*\.properties\.column5 | string | 
action\_result\.data\.\*\.properties\.function | string | 
action\_result\.data\.\*\.properties\.hasAgent | boolean | 
action\_result\.data\.\*\.properties\.lastSeen | string | 
action\_result\.data\.\*\.properties\.createdAt | string | 
action\_result\.data\.\*\.properties\.firstSeen | string | 
action\_result\.data\.\*\.properties\.networkId | string | 
action\_result\.data\.\*\.properties\.updatedAt | string | 
action\_result\.data\.\*\.properties\.networkName | string | 
action\_result\.data\.\*\.properties\.macAddresses | string | 
action\_result\.data\.\*\.properties\.netbiosNames | string | 
action\_result\.data\.\*\.properties\.tag\.Scan Group | string | 
action\_result\.data\.\*\.properties\.operatingSystems | string | 
action\_result\.data\.\*\.properties\.servicenowSysid | string | 
action\_result\.data\.\*\.properties\.hasPluginResults | boolean | 
action\_result\.data\.\*\.properties\.fqdns | string | 
action\_result\.data\.\*\.properties\.ipv4s | string | 
action\_result\.data\.\*\.properties\.lastScanTime | string | 
action\_result\.data\.\*\.properties\.firstScanTime | string | 
action\_result\.data\.\*\.properties\.lastLicensedScanDate | string | 
action\_result\.data\.\*\.properties\.lastScanId | string | 
action\_result\.data\.\*\.properties\.lastScheduleId | string | 
action\_result\.data\.\*\.count\(Record\) | numeric | 
action\_result\.data\.\*\.properties\.awsVpcId | string | 
action\_result\.data\.\*\.properties\.awsRegion | string | 
action\_result\.data\.\*\.properties\.awsOwnerId | string | 
action\_result\.data\.\*\.properties\.awsSubnetId | string | 
action\_result\.data\.\*\.properties\.awsEc2InstanceId | string | 
action\_result\.data\.\*\.properties\.awsEc2ProductCode | string | 
action\_result\.data\.\*\.properties\.awsEc2InstanceType | string | 
action\_result\.data\.\*\.properties\.awsAvailabilityZone | string | 
action\_result\.data\.\*\.properties\.awsEc2InstanceAmiId | string | 
action\_result\.data\.\*\.properties\.awsEc2InstanceState | string | 
action\_result\.data\.\*\.properties\.awsEc2InstanceGroupName | string | 
action\_result\.data\.\*\.properties\.lastAuthenticatedScanDate | string | 
action\_result\.data\.\*\.properties\.azureVmId | string | 
action\_result\.data\.\*\.properties\.azureResourceId | string | 
action\_result\.data\.\*\.properties\.tag\.bob | string | 
action\_result\.data\.\*\.properties\.tag\.Nick | string | 
action\_result\.data\.\*\.properties\.tag\.Test | string | 
action\_result\.data\.\*\.properties\.agentUuid | string | 
action\_result\.data\.\*\.properties\.terminatedAt | string | 
action\_result\.data\.\*\.properties\.terminatedBy | string | 
action\_result\.data\.\*\.properties\.ipv6s | string | 
action\_result\.data\.\*\.properties\.awsEc2Name | string | 
action\_result\.data\.\*\.properties\.installedSoftware | string | 
action\_result\.data\.\*\.properties\.tag\.foo | string | 
action\_result\.data\.\*\.properties\.biosUuid | string | 
action\_result\.data\.\*\.properties\.gcpZone | string | 
action\_result\.data\.\*\.properties\.gcpProjectId | string | 
action\_result\.data\.\*\.properties\.gcpInstanceId | string | 
action\_result\.data\.\*\.properties\.tag\.sample | string | 
action\_result\.data\.\*\.properties\.agentNames | string | 
action\_result\.data\.\*\.entity\.\_endOn | string | 
action\_result\.status | string | 
action\_result\.message | string | 
action\_result\.summary\.total\_results | numeric | 
summary\.total\_objects | numeric | 
summary\.total\_objects\_successful | numeric | 