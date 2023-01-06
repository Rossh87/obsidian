c.f. https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/

Plugins for API requests.  Admission controllers run after a request has been authenticated and authorized, and may either mutate an object or objects (a *mutating controller*), or further scrutinize the request (a *validating controller*), or both.  

For example, AlwaysPullImages will set the image pull policy for all created [[Pod]]s to `always`, regardless of what is specified in the request/specification (e.g. in a `yaml` file).

Note that admission controllers are not applied retroactively: objects will have the configuration they were created with regardless of any mutating controllers put in place **after** the object is created.  For example, a pod with `imagePullPolicy` set to `IfNotPresent` will still have that policy even if an `AlwaysPullImages` admission controller is later enabled.