# Azure Active Directory reports and monitoring

## Risk details field

_Licensing_: P2

The [sign-in log schema](https://docs.microsoft.com/azure/active-directory/reports-monitoring/reference-azure-monitor-sign-ins-log-schema#field-descriptions) includes the riskDetail field. This filed provides the reason behind a specific state of a risky user, sign-in or a risk detection. The possible values are: _none_, _adminGeneratedTemporaryPassword_, _userPerformedSecuredPasswordChange_, _userPerformedSecuredPasswordReset_, _adminConfirmedSigninSafe_, _aiConfirmedSigninSafe_, _userPassedMFADrivenByRiskBasedPolicy_, _adminDismissedAllRiskForUser_, _adminConfirmedSigninCompromised_, _unknownFutureValue_. The value none means that no action has been performed on the user or sign-in so far. 