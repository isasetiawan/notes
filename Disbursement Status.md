| Disbursement Transaction Status | Definition                                                                                                                         | Exist |
| ------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ----- |
| Waiting to Process              | the transaction status is in the uploading process                                                                                 | ✅     |
| In Progress                     | the transaction status after it has been successfully created                                                                      | ✅     |
| In Queue                        | the transaction is on the queue before successfully sending it to the disbursement vendor                                          | ✅     |
| In Retry Queue                  | the status for the retry mechanism of the transaction status has failed to be sent to the vendor                                   | ✅     |
| Completed                       | the transaction status after successfully disbursed by the vendor                                                                  | ✅     |
| Deleted                         | the transaction status when it is automatically deleted by the vendor systems due to some errors in their side (3rd party’s issue) |       |
| Rejected                        | the transaction status after being rejected by the admin in the vendor system / dashboard                                          | ✅     |
| Failed                          | the transaction status after failed to be disbursed by the vendor                                                                  | ✅     |
| Reversed                        | the transaction status after failed to be disbursed to the beneficiary accounts and being returned                                 |       |
