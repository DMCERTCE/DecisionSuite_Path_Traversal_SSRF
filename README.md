# DecisionSuite_Path_Traversal_SSRF

In TARGIT Decision Suite a serious vulnerability is present when using the VFS file fetching feature.
As demonstrated below prepending // to the path will allow browse other SMB paths using the service-account privileges.

POST /anywhere/Documents/Open?id=vfs%3A%2F%2F//localhost%2Fc%24%2FProgramData%2FTARGIT

This opens up a world of pain, as it allows the following:

- Recon of the internal network by using the SSRF (non-allowed filetypes will throw a unsupported file error) 

- Import of own code in the native Targit format.

- Access to reports inside of TARGIT (the report name can be fuzzed)

- Credential Theft of service account by using tools like responder or ntlmrelayx.

After dialogue with vendor it appears that this practice has been deprecated in the latest release.
