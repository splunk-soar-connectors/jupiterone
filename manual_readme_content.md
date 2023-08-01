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
