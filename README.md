<p><strong>Microsoft Azure &ndash; Monitor Static Web App using Front Door and Alerts.</strong></p>
<p>&nbsp;</p>
<p>This is a guide to improve the reliability of the Static Web Apps (SWA) by implementing monitoring, custom alerts, custom domain, front door configuration, and setup of all the environment.</p>
<p>&nbsp;</p>
<p>Resources needed:</p>
<ul>
<li>Custom domain and DNS zone previously created.</li>
<li>Static Web App - Standard.</li>
<li>Front Door &ndash; Standard/Premium.</li>
<li>GitHub repository.</li>
</ul>
<p>&nbsp;</p>
<p><strong>Section 1 &ndash; Creating the Static Web App.</strong></p>
<p>&nbsp;</p>
<p>Let&rsquo;s create a new resource group.</p>
<p>&nbsp;</p>
<p>Then let&rsquo;s create a new repository on GitHub and upload the Static Web App content:</p>
<p>&nbsp;</p>
<p>Then, create the Static Web App in the Azure portal.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Fill the required data:</p>
<p>After the creation of the Static Web App, go to the GitHub portal and check the Actions, verify that there is no problem to run the workflow.</p>
<p>&nbsp;</p>
<p>Then, you will be able to visit your new Static Web App using the Funny Name (default URL of the SWA).</p>
<p>&nbsp;</p>
<p>Let&rsquo;s recap:</p>
<p>We have created a new GitHub repository, then a SWA and deployed the content.</p>
<p>&nbsp;</p>
<p><strong>&nbsp;</strong></p>
<p><strong>Section 2 &ndash; Creating the Azure Front Door.</strong></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Go back to the resource group, at this point we have only the SWA, so we are going to create the Azure Front Door.</p>
<p>Click on&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; , in the Market place look up for Front Door and CDN profiles:</p>
<table>
<tbody>
<tr>
<td width="428">&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;&nbsp; Create the resource</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp; With this settings:</p>
<table>
<tbody>
<tr>
<td width="244">&nbsp;</td>
<td width="152">&nbsp;</td>
<td width="34">&nbsp;</td>
<td width="221">&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td colspan="2">&nbsp;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Configure the Front Door information and create the resource:</p>
<p>&nbsp;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>
<p>Now the Front Door is created</p>
<p>&nbsp;</p>
<p>Let&rsquo;s recap: We have created the SWA and the Azure Front Door.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>Section 3 &ndash; Configuration of the Front Door.</strong></p>
<p>&nbsp;</p>
<p>Let configure the Front Door to be able to reach the Static Web App.</p>
<p>Go to Front Door manager</p>
<p>You will see that there is an Endpoint configured and also the Security policy:</p>
<p><strong>&nbsp;</strong></p>
<p>Use the default endpoint URL to go to your SWA through the Azure Front Door (use https://&lt;URL&gt;)</p>
<p>&nbsp;</p>
<p>Now the SWA is configured to use a Front Door, and the Front Door is able to reach the SWA.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Let&rsquo;s improve the security by modify the Front Door endpoint to allow connections only under HTTPS protocol.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>In Accepted protocols select HTTPS only:</p>
<p>&nbsp;</p>
<p>In Forwarding protocol, change from Match incoming request option to HTTPS only:</p>
<p>Then, click on update&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;to apply the changes</p>
<p>&nbsp;</p>
<p>Now let configure the Static Web App to allow connection only from the Front Door by modifying the staticwebapp.config.json file:</p>
<p>Go to the GitHub repository, open the staticwebapp.config.json file:</p>
<p>Then click on &lsquo;Edit&rsquo; button</p>
<p>Add this lines:</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp; "networking": {</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "allowedIpRanges": ["AzureFrontDoor.Backend"]</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp; },</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Check the Actions tab of the repository:</p>
<p>&nbsp;</p>
<p>Now, if you want to go to the Static Web App using the Funny Name (custom URL), you will get a Forbidden message:</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>Section 4 &ndash; Configuring custom domain for Front Door Endpoint.</strong></p>
<p>Go to Front Door manager</p>
<p>&nbsp;</p>
<p>Click on Edit route</p>
<p>&nbsp;</p>
<p>In the Domain section, click on Add new domain</p>
<p>Select the DNS Zone</p>
<table>
<tbody>
<tr>
<td width="126">
<table width="100%">
<tbody>
<tr>
<td>
<p>DNS Zone</p>
</td>
</tr>
</tbody>
</table>
&nbsp;</td>
</tr>
</tbody>
</table>
<table>
<tbody>
<tr>
<td width="205">
<table width="100%">
<tbody>
<tr>
<td>
<p>Select the subscription</p>
</td>
</tr>
</tbody>
</table>
&nbsp;</td>
</tr>
</tbody>
</table>
<p>Click on Add new, to create the custom domain, or select one from the list.</p>
<p>You will get this alert:</p>
<p>The domain needs to be validated.</p>
<p>&nbsp;</p>
<p>Click on add.</p>
<p>&nbsp;</p>
<p>Then you will see both domains available for your endpoint:</p>
<p>You can choose if maintain both or disable the default domain.</p>
<p>&nbsp;</p>
<p>Click on Update to apply the changes.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>After applying the changes, you will see the second domain listed in the endpoint:</p>
<p>&nbsp;</p>
<p>Click on the domain, then you will see that the domain validation is needed and the validation state is Pending</p>
<p>Click on the Pending link, this will open a menu to Validate the custom domain:</p>
<table>
<tbody>
<tr>
<td width="218">&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<p><br /> Now click on Add, this action will create a TXT record on your DNS Zone (takes 5-10 minutes).</p>
<p>&nbsp;</p>
<p>Then click on Domain validation needed on Certificate static, and click on update.</p>
<p>After this step, you will need to wait around 10-20 minutes to complete the process of validation.</p>
<p>Additionally, you can add an extra CNAME record on your DNS Zone, the previous custom domain but pointing to the default URL of the endpoint.</p>
<p>When the verification concludes, you will be able to see your both custom domains for your endpoint:</p>
<p>Now we can go to the Static Web App using the custom domain configured to the endpoint (make sure you are using HTTPS protocol on the URL):</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>Section 5 &ndash; Configuring the alert for 4XX responses.</strong></p>
<p>&nbsp;</p>
<p>In the left panel menu, under monitoring section go to Alerts, then click on Action groups, then create.<br /> </p>
<table>
<tbody>
<tr>
<td width="285">&nbsp;</td>
<td width="45">&nbsp;</td>
<td width="199">&nbsp;</td>
<td width="44">&nbsp;</td>
</tr>
<tr>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
<td>&nbsp;</td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Fill the information</p>
<p>&nbsp;</p>
<p>Move to the Notifications tab:</p>
<p>&nbsp;</p>
<p>Then configure the email information:</p>
<p>After configured the email information, move to Review + create and create the action group, after that wait a few minutes to see the action group created.</p>
<p>&nbsp;</p>
<p>Now go to Alerts, Create and select Alert rule:</p>
<p>Select Percentage of 4XX</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Then configure the configure the Condition</p>
<p>Configure the Split by dimensions: Endpoint = your endpoint previously configured:</p>
<p>Then move to the Actions tab and select the action group recently created </p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Then move to the Details tab, configure then</p>
<p>Review and create:</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>
<p>&nbsp;</p>
<p>After that the rule will be created.</p>
<p>&nbsp;</p>
<p>For testing the alert, we can configure the staticwebapp.config.json to require authentication, as we did not configured any auth method in the SWA, the SWA will return a 401 Unauthorized, this will trigger the alert and the email alert will be sent.</p>
<p>&nbsp;</p>
<p>Let&rsquo;s configure the test:</p>
<p>Go to GitHub and modify the staticwebapp.config.json and add a property to allow only authenticated users by adding this property:</p>
<p>"routes": [</p>
<p>&nbsp;&nbsp;&nbsp; {</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "route": "/*",</p>
<p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; "allowedRoles": ["authenticated"]</p>
<p>&nbsp;&nbsp;&nbsp; }</p>
<p>&nbsp; ],</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>After adding the rule, check the workflow:</p>
<p>To trigger the alert go to the SWA and refresh the page:</p>
<p>&nbsp;</p>
<p>This will trigger the alert, then in about 5-10 minutes, the alert will get received on the email:</p>
<p>&nbsp;</p>
<p>It is possible to see the alert in the portal:</p>
<p>To re-enable your app to be accessible for all the customers, only remove the auth configuration from the staticwebapp.config.json.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>Let&rsquo;s recap: At this point we have configured the Static Web App, the GitHub repository, the Front Door, the endpoint with custom domain, the alerts.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>Section 6 &ndash; Documentation.<br /> <br /> </strong></p>
<p>Configure Azure Static Web Apps:</p>
<p><a href="https://learn.microsoft.com/en-us/azure/static-web-apps/configuration">Configure Azure Static Web Apps | Microsoft Learn</a>.</p>
<p>&nbsp;</p>
<p>Manually configure Azure Front Door for Azure Static Web Apps:</p>
<p><a href="https://learn.microsoft.com/en-us/azure/static-web-apps/front-door-manual">Tutorial: Manually configure Azure Front Door for Azure Static Web Apps | Microsoft Learn</a>.</p>
<p>&nbsp;</p>
<p>Azure Front Door:</p>
<p><a href="https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview">Azure Front Door | Microsoft Learn</a>.</p>
<p>&nbsp;</p>
<p>Custom domain with Azure DNS in Azure Static Web Apps:</p>
<p><a href="https://learn.microsoft.com/en-us/azure/static-web-apps/custom-domain-azure-dns">Set up a custom domain with Azure DNS in Azure Static Web Apps | Microsoft Learn</a></p>
<p>&nbsp;</p>
<p>Custom domain &ndash; Azure Front Door:</p>
<p><a href="https://techcommunity.microsoft.com/t5/fasttrack-for-azure/tips-and-tricks-to-perform-custom-domain-operations-in-azure/ba-p/3430908#:~:text=Steps%20to%20add%20a%20custom%20domain%20on%20Azure,custom%20domain%20is%20being%20created.%20...%20More%20items">Perform custom domain operations in Azure Front Door - Microsoft Community Hub</a></p>
