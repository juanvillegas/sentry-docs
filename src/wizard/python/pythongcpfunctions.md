---
name: GCP Cloud Functions
doc_link: https://docs.sentry.io/platforms/python/guides/gcp-functions/
support_level: production
type: framework
---

Install our Python SDK using `pip`:

```bash
$ pip install --upgrade sentry-sdk
```

You can use the GCP Functions integration for the Python SDK like this:

```python
import sentry_sdk
from sentry_sdk.integrations.gcp import GcpIntegration

sentry_sdk.init(
    dsn="___PUBLIC_DSN___",
    integrations=[GcpIntegration()],
)

def http_function_entrypoint(request):
    ...
```

Checkout Sentry's [GCP sample apps](https://github.com/getsentry/examples/tree/master/gcp-cloud-functions) for detailed examples.

### Enable Timeout Warning
Update the sentry initialization to set ```timeout_warning``` to ```true```
```python
sentry_sdk.init(
    dsn="___PUBLIC_DSN___",
    integrations=[GcpIntegration(timeout_warning=True)],
)
```
The timeout warning is sent only if the "timeout" in the GCP Function configuration is set to a value greater than one second.

<div class="alert alert-info" role="alert"><h5 class="no_toc">Note</h5><div class="alert-body content-flush-bottom">If you are using another web framework inside of GCP Functions, the framework might catch those exceptions before we get to see them. Make sure to enable the framework specific integration as well, if one exists. See [*Integrations*](/platforms/python/#integrations) for more information.</div>
</div>
