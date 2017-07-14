### Module Description
This module is a generic interface for event pushing backends.
It defines a single hook, `push_event/3` that forwards the event to all registered backends.
Each backend decides how and if to handle the event in its `push_event/2` implementation.

The events are standardized as records that can be found in `mod_event_pusher_events.hrl` file.
Common events like user presence change (offline and online), chat and groupchat messages (incoming and outgoing) are already hooked up to the frontend via `mod_event_pusher_hook_translator` that translates various hooks into specific calls of the `push_event/3` hook.

### Options

* **backends** (required, list) - Specifies backends to register with the frontend, along with arguments that will be passed to the backend.
Currently supported backends include [sns] and [push].
Refer to their specific documentation to learn more about their function and configuration option.

### Example configuration

```Erlang
{mod_event_pusher, [
    {backends, [
        {sns, [
            {access_key_id, "AKIAIOSFODNN7EXAMPLE"},
            {secret_access_key, "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"},
            % ...
        ]},
        {push, [
            {backend, mnesia},
            {wpool, [{workers, 200}]},
            {plugin_module, mod_push_plugin_default}
        ]}
    ]}
]}
```

[sns]: ./mod_aws_sns/
[push]: ./mod_push/
