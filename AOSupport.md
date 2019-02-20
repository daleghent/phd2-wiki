### PHD2 Supported AO Devices ###

Please help us keep this page up to date!  You can edit this page if you have a github account.  If you do not have a github account and do not want to get one, then please post on the [PHD2 Forum](https://groups.google.com/forum/?fromgroups=#!forum/open-phd-guiding) and let us know what you would like to see updated.

|AO|Windows|OSX|Linux|Notes|
|------|:-----:|:-:|:---:|-----|
| SBIG AO (INDI) | **Yes** | **Yes** | **Yes** | [note](#SBIG) |
| Starlight Xpress AO |  **Yes** | **Yes** | **Yes** | natively supported by PHD2,<br>also accessible via INDI |

<a name="SBIG"></a>
### SBIG AO ###
The SBIG Driver only allows a single application to connect to _all_ SBIG gear. If your imaging application is connected to an SBIG camera, then PHD2 cannot connect to the AO.  The SBIG AO is however accessible via INDI.
