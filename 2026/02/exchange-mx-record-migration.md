### Migrating Exchange to the New `mx.microsoft` MX Record

Updating the MX record for an Exchange mailbox from the legacy `mail.protection.outlook.com` to the new DNSSEC-enabled `mx.microsoft` record is a straightforward process. Here are the detailed steps:

1.  **Install the Exchange Online PowerShell Module**
    Open PowerShell on Windows and execute the following commands sequentially:
    ```powershell
    Set-ExecutionPolicy RemoteSigned
    Install-Module -Name ExchangeOnlineManagement -RequiredVersion 3.6.0
    Import-Module ExchangeOnlineManagement # This step is optional
    ```

2.  **Connect to Exchange Online**
    *   **For International/Global version users, run:**
        ```powershell
        Connect-ExchangeOnline
        ```
    *   **For the China version (e.g., operated by 21Vianet), run:**
        ```powershell
        Connect-ExchangeOnline -ExchangeEnvironmentName O365China
        ```
    Follow the prompts to log in with your administrator account.

3.  **Enable DNSSEC and Obtain the New MX Record**
    Run the following command, replacing `<DomainName>` with your actual domain name:
    ```powershell
    Enable-DnssecForVerifiedDomain -DomainName <DomainName>
    ```
    After a few seconds, you should receive a result similar to:
    ```
    Domain     MxValue                                   Result  ErrorData
    ------     -------                                   ------  ---------
    example.com example-com.a-v1.mx.microsoft           Success
    ```

4.  **Update the DNS Record**
    In your domain's DNS management console, replace the existing MX record with the new value returned in the previous step (e.g., `example-com.a-v1.mx.microsoft`).

**Additional Notes:**

*   Some domain providers might already show the new `mx.microsoft` record when adding an MX record. However, some users (including myself, based on tests with several domains) might still see the legacy `outlook.com` record. After the update, the actual A/AAAA records pointed to do not change.
*   According to Microsoft documentation, Exchange Online actually supports adding the following four MX records simultaneously (all in example format; replace with your actual domain prefix). This was also observed in the certificate with Serial Number `0c:0a:2b:08:93:5e:f5:0b:3d:d4:24:0a:e3:50:3f:b1`:
    *   `example-com.mail.protection.outlook.com`
    *   `example-com.mail.eo.outlook.com`
    *   `example-com.mail.protection.outlook.de`
    *   `example-com.a-v1.mx.microsoft`
    The A/AAAA records for `mail.protection.outlook.de` point to German IPs, likely intended for the EU region.

**References:**
*   <https://learn.microsoft.com/zh-cn/purview/how-smtp-dane-works>
*   <https://www.cnblogs.com/yujianadu/p/17586759.html>

