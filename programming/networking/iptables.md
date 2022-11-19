`iptables` is a firewall and NAT service.  It uses three different chains.  A chain is a sequence of policies that will be tested sequentially for all incoming and outgoing communication, and communications that match the rules specified for the policy will be applied.  The types of `chain` are:
1. `Input` governs packets that originate on a different host.
2. `Forward` governs packets that originate on a different host, but are *not* going to be delivered locally.
3. `Output` governs packets that originate on the host.

Keep in mind that most [[TCP]] connections will be affected by `OUTPUT` as well as `INPUT`, since they work on a req/res cycle.

All chains specify a default `policy` that will apply to connections that do not match any more-specific rule in the chain.

Rules are matched according to the line-order of the file.  As soon as a rule is matched, it is applied.  Depending on whether the rule has a *target* or a *decision*, further rules may or may not be evaluated.