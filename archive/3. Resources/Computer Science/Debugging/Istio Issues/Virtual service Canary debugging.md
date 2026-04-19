
sre-testing-can-app-sit / sre-testing-can-app-gw- flagger
	  http:
	  - route:
	    - destination:
	        host: sre-testing-can-app-sit-primary
	      weight: 100
	    - destination:
	        host: sre-testing-can-app-sit-canary
	      weight: 0
sre-testing-can-app-vs / sre-testing-can-app-gw- helm
	  http:
	  - match:
	    - port: 5001
	    route:
	    - destination:
	        host: sre-testing-can-app-sit
	        port:
	          number: 5001
	  - match:
	    - uri:
	        prefix: /
	    route:
	    - destination:
	        host: sre-testing-can-app-sit
	        port:
	          number: 80
```json
[
    {
        "name": "0.0.0.0_80",
        "address": {
            "socketAddress": {
                "address": "0.0.0.0",
                "portValue": 80
            }
        },
        "filterChains": [
            {
                "filterChainMatch": {
                    "transportProtocol": "raw_buffer",
                    "applicationProtocols": [
                        "http/1.0",
                        "http/1.1",
                        "h2c"
                    ]
                },
                "filters": [
                    {
                        "name": "envoy.filters.network.http_connection_manager",
                        "typedConfig": {
                            "@type": "type.googleapis.com/envoy.extensions.filters.network.http_connection_manager.v3.HttpConnectionManager",
                            "statPrefix": "outbound_0.0.0.0_80",
                            "rds": {
                                "configSource": {
                                    "ads": {},
                                    "initialFetchTimeout": "0s",
                                    "resourceApiVersion": "V3"
                                },
                                "routeConfigName": "80"
                            },
                            "httpFilters": [
                                {
                                    "name": "istio.metadata_exchange",
                                    "typedConfig": {
                                        "@type": "type.googleapis.com/envoy.extensions.filters.http.wasm.v3.Wasm",
                                        "config": {
                                            "vmConfig": {
                                                "runtime": "envoy.wasm.runtime.null",
                                                "code": {
                                                    "local": {
                                                        "inlineString": "envoy.wasm.metadata_exchange"
                                                    }
                                                }
                                            },
                                            "configuration": {
                                                "@type": "type.googleapis.com/envoy.tcp.metadataexchange.config.MetadataExchange"
                                            }
                                        }
                                    }
                                },
                                {
                                    "name": "istio.alpn",
                                    "typedConfig": {
                                        "@type": "type.googleapis.com/istio.envoy.config.filter.http.alpn.v2alpha1.FilterConfig",
                                        "alpnOverride": [
                                            {
                                                "alpnOverride": [
                                                    "istio-http/1.0",
                                                    "istio",
                                                    "http/1.0"
                                                ]
                                            },
                                            {
                                                "upstreamProtocol": "HTTP11",
                                                "alpnOverride": [
                                                    "istio-http/1.1",
                                                    "istio",
                                                    "http/1.1"
                                                ]
                                            },
                                            {
                                                "upstreamProtocol": "HTTP2",
                                                "alpnOverride": [
                                                    "istio-h2",
                                                    "istio",
                                                    "h2"
                                                ]
                                            }
                                        ]
                                    }
                                },
                                {
                                    "name": "envoy.filters.http.fault",
                                    "typedConfig": {
                                        "@type": "type.googleapis.com/envoy.extensions.filters.http.fault.v3.HTTPFault"
                                    }
                                },
                                {
                                    "name": "envoy.filters.http.cors",
                                    "typedConfig": {
                                        "@type": "type.googleapis.com/envoy.extensions.filters.http.cors.v3.Cors"
                                    }
                                },
                                {
                                    "name": "istio.stats",
                                    "typedConfig": {
                                        "@type": "type.googleapis.com/udpa.type.v1.TypedStruct",
                                        "typeUrl": "type.googleapis.com/envoy.extensions.filters.http.wasm.v3.Wasm",
                                        "value": {
                                            "config": {
                                                "configuration": {
                                                    "@type": "type.googleapis.com/google.protobuf.StringValue",
                                                    "value": "{\"metrics\":[{\"dimensions\":{\"request_method\":\"request.method\",\"request_url_path\":\"request.url_path\"},\"name\":\"requests_total\"}]}\n"
                                                },
                                                "root_id": "stats_outbound",
                                                "vm_config": {
                                                    "code": {
                                                        "local": {
                                                            "inline_string": "envoy.wasm.stats"
                                                        }
                                                    },
                                                    "runtime": "envoy.wasm.runtime.null",
                                                    "vm_id": "stats_outbound"
                                                }
                                            }
                                        }
                                    }
                                },
                                {
                                    "name": "envoy.filters.http.router",
                                    "typedConfig": {
                                        "@type": "type.googleapis.com/envoy.extensions.filters.http.router.v3.Router"
                                    }
                                }
                            ],
                            "tracing": {
                                "clientSampling": {
                                    "value": 100
                                },
                                "randomSampling": {
                                    "value": 100
                                },
                                "overallSampling": {
                                    "value": 100
                                },
                                "customTags": [
                                    {
                                        "tag": "istio.authorization.dry_run.allow_policy.name",
                                        "metadata": {
                                            "kind": {
                                                "request": {}
                                            },
                                            "metadataKey": {
                                                "key": "envoy.filters.http.rbac",
                                                "path": [
                                                    {
                                                        "key": "istio_dry_run_allow_shadow_effective_policy_id"
                                                    }
                                                ]
                                            }
                                        }
                                    },
                                    {
                                        "tag": "istio.authorization.dry_run.allow_policy.result",
                                        "metadata": {
                                            "kind": {
                                                "request": {}
                                            },
                                            "metadataKey": {
                                                "key": "envoy.filters.http.rbac",
                                                "path": [
                                                    {
                                                        "key": "istio_dry_run_allow_shadow_engine_result"
                                                    }
                                                ]
                                            }
                                        }
                                    },
                                    {
                                        "tag": "istio.authorization.dry_run.deny_policy.name",
                                        "metadata": {
                                            "kind": {
                                                "request": {}
                                            },
                                            "metadataKey": {
                                                "key": "envoy.filters.http.rbac",
                                                "path": [
                                                    {
                                                        "key": "istio_dry_run_deny_shadow_effective_policy_id"
                                                    }
                                                ]
                                            }
                                        }
                                    },
                                    {
                                        "tag": "istio.authorization.dry_run.deny_policy.result",
                                        "metadata": {
                                            "kind": {
                                                "request": {}
                                            },
                                            "metadataKey": {
                                                "key": "envoy.filters.http.rbac",
                                                "path": [
                                                    {
                                                        "key": "istio_dry_run_deny_shadow_engine_result"
                                                    }
                                                ]
                                            }
                                        }
                                    },
                                    {
                                        "tag": "istio.canonical_revision",
                                        "literal": {
                                            "value": "latest"
                                        }
                                    },
                                    {
                                        "tag": "istio.canonical_service",
                                        "literal": {
                                            "value": "sre-testing-app"
                                        }
                                    },
                                    {
                                        "tag": "istio.mesh_id",
                                        "literal": {
                                            "value": "cluster.local"
                                        }
                                    },
                                    {
                                        "tag": "istio.namespace",
                                        "literal": {
                                            "value": "sre"
                                        }
                                    }
                                ]
                            },
                            "httpProtocolOptions": {
                                "acceptHttp10": true
                            },
                            "streamIdleTimeout": "0s",
                            "accessLog": [
                                {
                                    "name": "envoy.access_loggers.file",
                                    "typedConfig": {
                                        "@type": "type.googleapis.com/envoy.extensions.access_loggers.file.v3.FileAccessLog",
                                        "path": "/dev/stdout",
                                        "logFormat": {
                                            "jsonFormat": {
                                                "bytes_received": "%BYTES_RECEIVED%",
                                                "bytes_sent": "%BYTES_SENT%",
                                                "downstream_local_address": "%DOWNSTREAM_LOCAL_ADDRESS%",
                                                "downstream_remote_address": "%DOWNSTREAM_REMOTE_ADDRESS%",
                                                "duration": "%DURATION%",
                                                "log_type": "access_log",
                                                "method": "%REQ(:METHOD)%",
                                                "path": "%REQ(X-ENVOY-ORIGINAL-PATH?:PATH)%",
                                                "protocol": "%PROTOCOL%",
                                                "request_id": "%REQ(X-REQUEST-ID)%",
                                                "response_code": "%RESPONSE_CODE%",
                                                "response_flags": "%RESPONSE_FLAGS%",
                                                "start_time": "%START_TIME%",
                                                "upstream_cluster": "%UPSTREAM_CLUSTER%",
                                                "upstream_host": "%UPSTREAM_HOST%",
                                                "upstream_local_address": "%UPSTREAM_LOCAL_ADDRESS%",
                                                "upstream_service_time": "%RESP(X-ENVOY-UPSTREAM-SERVICE-TIME)%",
                                                "x_forwarded_for": "%REQ(X-FORWARDED-FOR)%"
                                            }
                                        }
                                    }
                                }
                            ],
                            "useRemoteAddress": false,
                            "upgradeConfigs": [
                                {
                                    "upgradeType": "websocket"
                                }
                            ],
                            "normalizePath": true,
                            "pathWithEscapedSlashesAction": "KEEP_UNCHANGED",
                            "requestIdExtension": {
                                "typedConfig": {
                                    "@type": "type.googleapis.com/envoy.extensions.request_id.uuid.v3.UuidRequestIdConfig",
                                    "useRequestIdForTraceSampling": true
                                }
                            }
                        }
                    }
                ]
            }
        ],
        "defaultFilterChain": {
            "filterChainMatch": {},
            "filters": [
                {
                    "name": "istio.stats",
                    "typedConfig": {
                        "@type": "type.googleapis.com/udpa.type.v1.TypedStruct",
                        "typeUrl": "type.googleapis.com/envoy.extensions.filters.network.wasm.v3.Wasm",
                        "value": {
                            "config": {
                                "configuration": {
                                    "@type": "type.googleapis.com/google.protobuf.StringValue",
                                    "value": "{\"metrics\":[{\"dimensions\":{\"request_method\":\"request.method\",\"request_url_path\":\"request.url_path\"},\"name\":\"requests_total\"}]}\n"
                                },
                                "root_id": "stats_outbound",
                                "vm_config": {
                                    "code": {
                                        "local": {
                                            "inline_string": "envoy.wasm.stats"
                                        }
                                    },
                                    "runtime": "envoy.wasm.runtime.null",
                                    "vm_id": "tcp_stats_outbound"
                                }
                            }
                        }
                    }
                },
                {
                    "name": "envoy.filters.network.tcp_proxy",
                    "typedConfig": {
                        "@type": "type.googleapis.com/envoy.extensions.filters.network.tcp_proxy.v3.TcpProxy",
                        "statPrefix": "PassthroughCluster",
                        "cluster": "PassthroughCluster",
                        "accessLog": [
                            {
                                "name": "envoy.access_loggers.file",
                                "typedConfig": {
                                    "@type": "type.googleapis.com/envoy.extensions.access_loggers.file.v3.FileAccessLog",
                                    "path": "/dev/stdout",
                                    "logFormat": {
                                        "jsonFormat": {
                                            "bytes_received": "%BYTES_RECEIVED%",
                                            "bytes_sent": "%BYTES_SENT%",
                                            "downstream_local_address": "%DOWNSTREAM_LOCAL_ADDRESS%",
                                            "downstream_remote_address": "%DOWNSTREAM_REMOTE_ADDRESS%",
                                            "duration": "%DURATION%",
                                            "log_type": "access_log",
                                            "method": "%REQ(:METHOD)%",
                                            "path": "%REQ(X-ENVOY-ORIGINAL-PATH?:PATH)%",
                                            "protocol": "%PROTOCOL%",
                                            "request_id": "%REQ(X-REQUEST-ID)%",
                                            "response_code": "%RESPONSE_CODE%",
                                            "response_flags": "%RESPONSE_FLAGS%",
                                            "start_time": "%START_TIME%",
                                            "upstream_cluster": "%UPSTREAM_CLUSTER%",
                                            "upstream_host": "%UPSTREAM_HOST%",
                                            "upstream_local_address": "%UPSTREAM_LOCAL_ADDRESS%",
                                            "upstream_service_time": "%RESP(X-ENVOY-UPSTREAM-SERVICE-TIME)%",
                                            "x_forwarded_for": "%REQ(X-FORWARDED-FOR)%"
                                        }
                                    }
                                }
                            }
                        ]
                    }
                }
            ],
            "name": "PassthroughFilterChain"
        },
        "listenerFilters": [
            {
                "name": "envoy.filters.listener.tls_inspector",
                "typedConfig": {
                    "@type": "type.googleapis.com/envoy.extensions.filters.listener.tls_inspector.v3.TlsInspector"
                }
            },
            {
                "name": "envoy.filters.listener.http_inspector",
                "typedConfig": {
                    "@type": "type.googleapis.com/envoy.extensions.filters.listener.http_inspector.v3.HttpInspector"
                }
            }
        ],
        "listenerFiltersTimeout": "0s",
        "continueOnListenerFiltersTimeout": true,
        "trafficDirection": "OUTBOUND",
        "accessLog": [
            {
                "name": "envoy.access_loggers.file",
                "filter": {
                    "responseFlagFilter": {
                        "flags": [
                            "NR"
                        ]
                    }
                },
                "typedConfig": {
                    "@type": "type.googleapis.com/envoy.extensions.access_loggers.file.v3.FileAccessLog",
                    "path": "/dev/stdout",
                    "logFormat": {
                        "jsonFormat": {
                            "bytes_received": "%BYTES_RECEIVED%",
                            "bytes_sent": "%BYTES_SENT%",
                            "downstream_local_address": "%DOWNSTREAM_LOCAL_ADDRESS%",
                            "downstream_remote_address": "%DOWNSTREAM_REMOTE_ADDRESS%",
                            "duration": "%DURATION%",
                            "log_type": "access_log",
                            "method": "%REQ(:METHOD)%",
                            "path": "%REQ(X-ENVOY-ORIGINAL-PATH?:PATH)%",
                            "protocol": "%PROTOCOL%",
                            "request_id": "%REQ(X-REQUEST-ID)%",
                            "response_code": "%RESPONSE_CODE%",
                            "response_flags": "%RESPONSE_FLAGS%",
                            "start_time": "%START_TIME%",
                            "upstream_cluster": "%UPSTREAM_CLUSTER%",
                            "upstream_host": "%UPSTREAM_HOST%",
                            "upstream_local_address": "%UPSTREAM_LOCAL_ADDRESS%",
                            "upstream_service_time": "%RESP(X-ENVOY-UPSTREAM-SERVICE-TIME)%",
                            "x_forwarded_for": "%REQ(X-FORWARDED-FOR)%"
                        }
                    }
                }
            }
        ],
        "bindToPort": false
    }
]
```