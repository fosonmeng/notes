# Deploying to IIS

## HTTP Error 405.0 - Method Not Allowed in IIS Express

```xml
# web.config
<system.webServer>
  <modules>
    <remove name="WebDAVModule" />
  </modules>
  <handlers>
    <add name="aspNetCore" path="*" verb="*" modules="AspNetCoreModuleV2" resourceType="Unspecified" />
    <remove name="WebDAV" />
  </handlers>
</system.webServer>
```