[Github](https://github.com/thewh1teagle/vibe)
Сама скачивает модели, есть инсталлятор, красивый UI, но вызывает у меня синий экран со стандартными настройками. Есть у него ещё серверный интерфейс. Можно было бы попробовать его подцепить к плагину Obsidian Whisper
В настройках можно поменять GPU device number.
![[Pasted image 20241007192417.png]]
Поменял на 1, т.к. у меня же ещё встройка. Синего экрана нет, но валится без ошибки. В логах тоже нет никакой явной ошибки.
> [!question]- Лог
> {"timestamp":"2024-10-07T11:19:39.939738Z","level":"DEBUG","fields":{"message":"Vibe App Running"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:39.940223Z","level":"DEBUG","fields":{"message":"webview version: 129.0.2792.79"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:39.940388Z","level":"DEBUG","fields":{"message":"Protocol handler registered successfully."},"target":"vibe::custom_protocol"}
{"timestamp":"2024-10-07T11:19:39.940425Z","level":"DEBUG","fields":{"message":"Cargo features: vulkan"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:39.940466Z","level":"DEBUG","fields":{"message":"CPU Features\n{\"avx\":{\"enabled\":true,\"support\":true},\"avx2\":{\"enabled\":true,\"support\":true},\"f16c\":{\"enabled\":true,\"support\":true},\"fma\":{\"enabled\":true,\"support\":true}}"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:39.941013Z","level":"DEBUG","fields":{"message":"Executable Architecture: x86_64"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:39.941030Z","level":"DEBUG","fields":{"message":"APP VERSION: 2.5.6"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:39.941036Z","level":"DEBUG","fields":{"message":"COMMIT HASH: 567b2342394db1ccc9bf9cdc22d16df534a26a80"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:39.941052Z","level":"DEBUG","fields":{"message":"Non CLI mode"},"target":"vibe::setup"}
{"timestamp":"2024-10-07T11:19:41.458140Z","level":"DEBUG","fields":{"message":"Vulkan support is successfully checked and working."},"target":"vibe::cmd"}
{"timestamp":"2024-10-07T11:19:41.518258Z","level":"TRACE","fields":{"message":"checkout waiting for idle connection: (\"https\", github.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:41.518388Z","level":"TRACE","fields":{"message":"Http::connect; scheme=Some(\"https\"), host=Some(\"github.com\"), port=None"},"target":"hyper_util::client::legacy::connect::http"}
{"timestamp":"2024-10-07T11:19:41.518659Z","level":"DEBUG","fields":{"message":"resolving","host":"github.com"},"target":"hyper_util::client::legacy::connect::dns","span":{"host":"github.com","name":"resolve"},"spans":[{"host":"github.com","name":"resolve"}]}
{"timestamp":"2024-10-07T11:19:41.535401Z","level":"DEBUG","fields":{"message":"connecting to 140.82.121.4:443"},"target":"hyper_util::client::legacy::connect::http"}
{"timestamp":"2024-10-07T11:19:41.537442Z","level":"DEBUG","fields":{"message":"Default Input Device:\nOk(\"Microphone (Realtek(R) Audio)\")"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:41.537471Z","level":"DEBUG","fields":{"message":"Default Output Device:\nOk(\"Speakers (Realtek(R) Audio)\")"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:41.538908Z","level":"DEBUG","fields":{"message":"Devices: "},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:41.643237Z","level":"DEBUG","fields":{"message":"connected to 140.82.121.4:443"},"target":"hyper_util::client::legacy::connect::http"}
{"timestamp":"2024-10-07T11:19:41.895103Z","level":"TRACE","fields":{"message":"http1 handshake complete, spawning background dispatcher task"},"target":"hyper_util::client::legacy::client"}
{"timestamp":"2024-10-07T11:19:41.895179Z","level":"TRACE","fields":{"message":"checkout dropped for (\"https\", github.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.136354Z","level":"TRACE","fields":{"message":"put; add idle connection for (\"https\", github.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.136385Z","level":"DEBUG","fields":{"message":"pooling idle connection for (\"https\", github.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.136440Z","level":"TRACE","fields":{"message":"take? (\"https\", github.com): expiration = Some(90s)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.136465Z","level":"DEBUG","fields":{"message":"reuse idle connection for (\"https\", github.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.136540Z","level":"TRACE","fields":{"message":"idle interval checking for expired"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.383639Z","level":"TRACE","fields":{"message":"put; add idle connection for (\"https\", github.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.383731Z","level":"DEBUG","fields":{"message":"pooling idle connection for (\"https\", github.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.383873Z","level":"TRACE","fields":{"message":"checkout waiting for idle connection: (\"https\", objects.githubusercontent.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:42.384039Z","level":"TRACE","fields":{"message":"Http::connect; scheme=Some(\"https\"), host=Some(\"objects.githubusercontent.com\"), port=None"},"target":"hyper_util::client::legacy::connect::http"}
{"timestamp":"2024-10-07T11:19:42.384206Z","level":"DEBUG","fields":{"message":"resolving","host":"objects.githubusercontent.com"},"target":"hyper_util::client::legacy::connect::dns","span":{"host":"objects.githubusercontent.com","name":"resolve"},"spans":[{"host":"objects.githubusercontent.com","name":"resolve"}]}
{"timestamp":"2024-10-07T11:19:42.392568Z","level":"DEBUG","fields":{"message":"connecting to 185.199.111.133:443"},"target":"hyper_util::client::legacy::connect::http"}
{"timestamp":"2024-10-07T11:19:42.503654Z","level":"DEBUG","fields":{"message":"connected to 185.199.111.133:443"},"target":"hyper_util::client::legacy::connect::http"}
{"timestamp":"2024-10-07T11:19:42.757283Z","level":"TRACE","fields":{"message":"http1 handshake complete, spawning background dispatcher task"},"target":"hyper_util::client::legacy::client"}
{"timestamp":"2024-10-07T11:19:42.757325Z","level":"TRACE","fields":{"message":"checkout dropped for (\"https\", objects.githubusercontent.com)"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:43.216936Z","level":"TRACE","fields":{"message":"pool closed, canceling idle interval"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:43.217062Z","level":"TRACE","fields":{"message":"pool dropped, dropping pooled ((\"https\", objects.githubusercontent.com))"},"target":"hyper_util::client::legacy::pool"}
{"timestamp":"2024-10-07T11:19:45.532247Z","level":"DEBUG","fields":{"message":"Recording from device: Microphone (Realtek(R) Audio)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.532309Z","level":"DEBUG","fields":{"message":"Device ID: 1"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.536897Z","level":"DEBUG","fields":{"message":"WAV file path: \"C:\\\\Users\\\\Valentin\\\\AppData\\\\Local\\\\Temp\\\\cHe1O0RR0f.wav\""},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.652625Z","level":"DEBUG","fields":{"message":"Stream started playing"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.652653Z","level":"DEBUG","fields":{"message":"Stream handle created"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.652666Z","level":"DEBUG","fields":{"message":"Recording from device: Speakers (Realtek(R) Audio)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.652671Z","level":"DEBUG","fields":{"message":"Device ID: 0"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.655302Z","level":"DEBUG","fields":{"message":"WAV file path: \"C:\\\\Users\\\\Valentin\\\\AppData\\\\Local\\\\Temp\\\\TXdHIpJVnC.wav\""},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.664385Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.674379Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.684372Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.694528Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.704588Z","level":"DEBUG","fields":{"message":"Stream started playing"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.704619Z","level":"DEBUG","fields":{"message":"Stream handle created"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.704708Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.715132Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.725067Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.735239Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.744552Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.754866Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.765083Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.775306Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.784643Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.794814Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.805019Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.815013Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.825045Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.835273Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.844734Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.855065Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.865033Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.875161Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.885285Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.894625Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.904774Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.915003Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.925128Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.935137Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.945396Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.954786Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.965032Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.975264Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.984436Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:45.995302Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.005525Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.015580Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.025568Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.035021Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.044875Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.055080Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.065054Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.075436Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.084349Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.095300Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.105329Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.115178Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.125185Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.135215Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.144636Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.154707Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.164700Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.174864Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.185032Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.195216Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.205263Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.215637Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.225355Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.235767Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.244986Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.254895Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.264912Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.275274Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.284784Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.294939Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.305176Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.314777Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.324937Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.335235Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.344519Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.354707Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.365015Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.375332Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.384473Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.394820Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.404920Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.415028Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.425391Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.434630Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.444920Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.455131Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.465163Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.474611Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.484871Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.494954Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.505196Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.515275Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.524596Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.534505Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.544516Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.554698Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.564784Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.574890Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.585076Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.594579Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.604704Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.614920Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.624817Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.635079Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.645068Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.655238Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.665067Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.674914Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.685009Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.695051Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.704294Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.714366Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.724375Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.734549Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.744716Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.755080Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.764554Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.774893Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.785041Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.794569Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.804975Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.815234Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.824587Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.834728Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.845556Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.856135Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.865609Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.875430Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.885473Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.895253Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.905199Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.914341Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.924723Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.934872Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.944999Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.954365Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.964344Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.974697Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.984926Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:46.995083Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.004517Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.014512Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.024679Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.035081Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.045328Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.054661Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.064759Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.074832Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.085033Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.095124Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.105334Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.114838Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.125017Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.135109Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.145245Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.154428Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.165240Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.175605Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.185570Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.195189Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.205187Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.214970Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.225084Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.235214Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.244657Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.254760Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.264831Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.275079Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.284374Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.294738Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.304977Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.315004Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.325316Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.334672Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.344651Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.355046Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.364360Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.374698Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.385040Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.394536Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.404656Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.414933Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.425258Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.435801Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.445267Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.455276Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.465348Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.475657Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.485031Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.495120Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.505239Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.515434Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.524954Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.535103Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.545473Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.554807Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.564972Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.575133Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.585247Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.595507Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.604297Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.614386Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.624761Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.634856Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.644958Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.655259Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.664496Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.674840Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.685098Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.695402Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.704834Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.715010Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.725346Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.735093Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.744520Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.754689Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.764855Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.775110Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.784557Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.794932Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.805222Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.814492Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.824792Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.835210Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.845538Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.854884Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.865005Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.875212Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.885414Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.894786Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.904970Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.915296Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.925321Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.935461Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.944921Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.955123Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.965307Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.975519Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.984692Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:47.995152Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.005427Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.015504Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.024983Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.035151Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.045481Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.055142Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.064844Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.075346Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.085587Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.094897Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.105049Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.115159Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.125706Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.135225Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.144456Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.154870Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.165080Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.175367Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.184777Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.194953Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.205147Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.215220Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.224563Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.234780Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.244679Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.254984Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.265044Z","level":"DEBUG","fields":{"message":"Writing input data (F32)"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.274761Z","level":"DEBUG","fields":{"message":"Pausing stream"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.274791Z","level":"DEBUG","fields":{"message":"Finalizing writer"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.286224Z","level":"DEBUG","fields":{"message":"Pausing stream"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.286255Z","level":"DEBUG","fields":{"message":"Finalizing writer"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.294150Z","level":"DEBUG","fields":{"message":"Emitting record_finish event"},"target":"vibe::cmd::audio"}
{"timestamp":"2024-10-07T11:19:48.294727Z","level":"DEBUG","fields":{"message":"ffmpeg path is C:\\Program Files\\ImageMagick-7.0.10-Q16-HDRI\\ffmpeg.exe"},"target":"vibe_core::audio"}

Использует установленный мною ffmpeg:
```
{"timestamp":"2024-10-07T11:19:48.294727Z","level":"DEBUG","fields":{"message":"ffmpeg path is C:\\Program Files\\ImageMagick-7.0.10-Q16-HDRI\\ffmpeg.exe"},"target":"vibe_core::audio"}
```
Мб надо взять удалить его из %PATH%? 
Удалил. Опять вылетело безо всяких ошибок в логе.

