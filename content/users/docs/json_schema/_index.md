---
title: "JSON Schema"
linkTitle: "JSON Schema"
weight: 50
---

<!-- Include from a free CDN -->
<script src="https://cdn.rawgit.com/caldwell/renderjson/master/renderjson.js"></script>

<!-- Element where the list will be created -->
<div id="container"></div>

<script>
    // The JSObject that you want to render
	var data = {
  "title": "RailJsonInfra",
  "type": "object",
  "properties": {
    "version": {
      "title": "Version",
      "enum": [
        "2.3.0"
      ],
      "type": "string"
    },
    "operational_points": {
      "title": "Operational Points",
      "type": "array",
      "items": {
        "$ref": "#/definitions/OperationalPoint"
      }
    },
    "routes": {
      "title": "Routes",
      "type": "array",
      "items": {
        "$ref": "#/definitions/Route"
      }
    },
    "switch_types": {
      "title": "Switch Types",
      "type": "array",
      "items": {
        "$ref": "#/definitions/SwitchType"
      }
    },
    "switches": {
      "title": "Switches",
      "type": "array",
      "items": {
        "$ref": "#/definitions/Switch"
      }
    },
    "track_section_links": {
      "title": "Track Section Links",
      "type": "array",
      "items": {
        "$ref": "#/definitions/TrackSectionLink"
      }
    },
    "track_sections": {
      "title": "Track Sections",
      "type": "array",
      "items": {
        "$ref": "#/definitions/TrackSection"
      }
    },
    "speed_sections": {
      "title": "Speed Sections",
      "type": "array",
      "items": {
        "$ref": "#/definitions/SpeedSection"
      }
    },
    "catenaries": {
      "title": "Catenaries",
      "type": "array",
      "items": {
        "$ref": "#/definitions/Catenary"
      }
    },
    "signals": {
      "title": "Signals",
      "type": "array",
      "items": {
        "$ref": "#/definitions/Signal"
      }
    },
    "buffer_stops": {
      "title": "Buffer Stops",
      "type": "array",
      "items": {
        "$ref": "#/definitions/BufferStop"
      }
    },
    "detectors": {
      "title": "Detectors",
      "type": "array",
      "items": {
        "$ref": "#/definitions/Detector"
      }
    }
  },
  "required": [
    "version",
    "operational_points",
    "routes",
    "switch_types",
    "switches",
    "track_section_links",
    "track_sections",
    "speed_sections",
    "catenaries",
    "signals",
    "buffer_stops",
    "detectors"
  ],
  "definitions": {
    "ObjectReference": {
      "title": "ObjectReference",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "type": {
          "title": "Type",
          "type": "string"
        }
      },
      "required": [
        "id",
        "type"
      ]
    },
    "OperationalPointPart": {
      "title": "OperationalPointPart",
      "type": "object",
      "properties": {
        "track": {
          "$ref": "#/definitions/ObjectReference"
        },
        "position": {
          "title": "Position",
          "type": "number"
        }
      },
      "required": [
        "track",
        "position"
      ]
    },
    "OperationalPoint": {
      "title": "OperationalPoint",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "parts": {
          "title": "Parts",
          "type": "array",
          "items": {
            "$ref": "#/definitions/OperationalPointPart"
          }
        },
        "ci": {
          "title": "Ci",
          "type": "integer"
        },
        "ch": {
          "title": "Ch",
          "maxLength": 2,
          "type": "string"
        },
        "ch_short_label": {
          "title": "Ch Short Label",
          "maxLength": 255,
          "type": "string"
        },
        "ch_long_label": {
          "title": "Ch Long Label",
          "maxLength": 255,
          "type": "string"
        },
        "name": {
          "title": "Name",
          "maxLength": 255,
          "type": "string"
        }
      },
      "required": [
        "id",
        "parts",
        "ci",
        "ch",
        "name"
      ]
    },
    "Direction": {
      "title": "Direction",
      "description": "An enumeration.",
      "enum": [
        "START_TO_STOP",
        "STOP_TO_START"
      ],
      "type": "string"
    },
    "DirectionalTrackRange": {
      "title": "DirectionalTrackRange",
      "type": "object",
      "properties": {
        "track": {
          "$ref": "#/definitions/ObjectReference"
        },
        "begin": {
          "title": "Begin",
          "type": "number"
        },
        "end": {
          "title": "End",
          "type": "number"
        },
        "direction": {
          "$ref": "#/definitions/Direction"
        }
      },
      "required": [
        "track",
        "begin",
        "end",
        "direction"
      ]
    },
    "Route": {
      "title": "Route",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "entry_point": {
          "$ref": "#/definitions/ObjectReference"
        },
        "exit_point": {
          "$ref": "#/definitions/ObjectReference"
        },
        "release_detectors": {
          "title": "Release Detectors",
          "type": "array",
          "items": {
            "$ref": "#/definitions/ObjectReference"
          }
        },
        "path": {
          "title": "Path",
          "type": "array",
          "items": {
            "$ref": "#/definitions/DirectionalTrackRange"
          }
        }
      },
      "required": [
        "id",
        "entry_point",
        "exit_point",
        "release_detectors",
        "path"
      ]
    },
    "SwitchPortConnection": {
      "title": "SwitchPortConnection",
      "type": "object",
      "properties": {
        "src": {
          "title": "Src",
          "type": "string"
        },
        "dst": {
          "title": "Dst",
          "type": "string"
        },
        "bidirectional": {
          "title": "Bidirectional",
          "type": "boolean"
        }
      },
      "required": [
        "src",
        "dst",
        "bidirectional"
      ]
    },
    "SwitchType": {
      "title": "SwitchType",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "ports": {
          "title": "Ports",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "groups": {
          "title": "Groups",
          "type": "object",
          "additionalProperties": {
            "type": "array",
            "items": {
              "$ref": "#/definitions/SwitchPortConnection"
            }
          }
        }
      },
      "required": [
        "id",
        "ports",
        "groups"
      ]
    },
    "Endpoint": {
      "title": "Endpoint",
      "description": "An enumeration.",
      "enum": [
        "BEGIN",
        "END"
      ],
      "type": "string"
    },
    "TrackEndpoint": {
      "title": "TrackEndpoint",
      "type": "object",
      "properties": {
        "endpoint": {
          "$ref": "#/definitions/Endpoint"
        },
        "track": {
          "$ref": "#/definitions/ObjectReference"
        }
      },
      "required": [
        "endpoint",
        "track"
      ]
    },
    "Switch": {
      "title": "Switch",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "switch_type": {
          "$ref": "#/definitions/ObjectReference"
        },
        "group_change_delay": {
          "title": "Group Change Delay",
          "type": "number"
        },
        "ports": {
          "title": "Ports",
          "type": "object",
          "additionalProperties": {
            "$ref": "#/definitions/TrackEndpoint"
          }
        },
        "label": {
          "title": "Label",
          "type": "string"
        }
      },
      "required": [
        "id",
        "switch_type",
        "group_change_delay",
        "ports",
        "label"
      ]
    },
    "ApplicableDirections": {
      "title": "ApplicableDirections",
      "description": "An enumeration.",
      "enum": [
        "START_TO_STOP",
        "STOP_TO_START",
        "BOTH"
      ],
      "type": "string"
    },
    "TrackSectionLink": {
      "title": "TrackSectionLink",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "src": {
          "$ref": "#/definitions/TrackEndpoint"
        },
        "dst": {
          "$ref": "#/definitions/TrackEndpoint"
        },
        "navigability": {
          "$ref": "#/definitions/ApplicableDirections"
        }
      },
      "required": [
        "id",
        "src",
        "dst",
        "navigability"
      ]
    },
    "LineString": {
      "title": "LineString",
      "description": "LineString Model",
      "type": "object",
      "properties": {
        "coordinates": {
          "title": "Coordinates",
          "minItems": 2,
          "type": "array",
          "items": {
            "anyOf": [
              {
                "type": "array",
                "minItems": 2,
                "maxItems": 2,
                "items": [
                  {
                    "anyOf": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "integer"
                      }
                    ]
                  },
                  {
                    "anyOf": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "integer"
                      }
                    ]
                  }
                ]
              },
              {
                "type": "array",
                "minItems": 3,
                "maxItems": 3,
                "items": [
                  {
                    "anyOf": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "integer"
                      }
                    ]
                  },
                  {
                    "anyOf": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "integer"
                      }
                    ]
                  },
                  {
                    "anyOf": [
                      {
                        "type": "number"
                      },
                      {
                        "type": "integer"
                      }
                    ]
                  }
                ]
              }
            ]
          }
        },
        "type": {
          "title": "Type",
          "const": "LineString",
          "type": "string"
        }
      },
      "required": [
        "coordinates"
      ]
    },
    "Slope": {
      "title": "Slope",
      "type": "object",
      "properties": {
        "gradient": {
          "title": "Gradient",
          "type": "number"
        },
        "begin": {
          "title": "Begin",
          "type": "number"
        },
        "end": {
          "title": "End",
          "type": "number"
        }
      },
      "required": [
        "gradient",
        "begin",
        "end"
      ]
    },
    "Curve": {
      "title": "Curve",
      "type": "object",
      "properties": {
        "radius": {
          "title": "Radius",
          "type": "number"
        },
        "begin": {
          "title": "Begin",
          "type": "number"
        },
        "end": {
          "title": "End",
          "type": "number"
        }
      },
      "required": [
        "radius",
        "begin",
        "end"
      ]
    },
    "LoadingGaugeType": {
      "title": "LoadingGaugeType",
      "description": "An enumeration.",
      "enum": [
        "G1",
        "G2",
        "GA",
        "GB",
        "GB1",
        "GC",
        "FR3.3",
        "FR3.3/GB/G2"
      ],
      "type": "string"
    },
    "ApplicableTrainType": {
      "title": "ApplicableTrainType",
      "description": "An enumeration.",
      "enum": [
        "FREIGHT",
        "PASSENGER"
      ],
      "type": "string"
    },
    "LoadingGaugeLimit": {
      "title": "LoadingGaugeLimit",
      "type": "object",
      "properties": {
        "category": {
          "$ref": "#/definitions/LoadingGaugeType"
        },
        "begin": {
          "title": "Begin",
          "type": "number"
        },
        "end": {
          "title": "End",
          "type": "number"
        },
        "applicable_train_type": {
          "$ref": "#/definitions/ApplicableTrainType"
        }
      },
      "required": [
        "category",
        "begin",
        "end",
        "applicable_train_type"
      ]
    },
    "TrackSection": {
      "title": "TrackSection",
      "type": "object",
      "properties": {
        "geo": {
          "$ref": "#/definitions/LineString"
        },
        "sch": {
          "$ref": "#/definitions/LineString"
        },
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "length": {
          "title": "Length",
          "type": "number"
        },
        "line_code": {
          "title": "Line Code",
          "type": "integer"
        },
        "line_name": {
          "title": "Line Name",
          "maxLength": 255,
          "type": "string"
        },
        "track_number": {
          "title": "Track Number",
          "type": "integer"
        },
        "track_name": {
          "title": "Track Name",
          "maxLength": 255,
          "type": "string"
        },
        "navigability": {
          "$ref": "#/definitions/ApplicableDirections"
        },
        "slopes": {
          "title": "Slopes",
          "type": "array",
          "items": {
            "$ref": "#/definitions/Slope"
          }
        },
        "curves": {
          "title": "Curves",
          "type": "array",
          "items": {
            "$ref": "#/definitions/Curve"
          }
        },
        "loading_gauge_limits": {
          "title": "Loading Gauge Limits",
          "type": "array",
          "items": {
            "$ref": "#/definitions/LoadingGaugeLimit"
          }
        }
      },
      "required": [
        "geo",
        "sch",
        "id",
        "length",
        "line_code",
        "line_name",
        "track_number",
        "track_name",
        "navigability",
        "slopes",
        "curves"
      ]
    },
    "ApplicableDirectionsTrackRange": {
      "title": "ApplicableDirectionsTrackRange",
      "type": "object",
      "properties": {
        "track": {
          "$ref": "#/definitions/ObjectReference"
        },
        "begin": {
          "title": "Begin",
          "type": "number"
        },
        "end": {
          "title": "End",
          "type": "number"
        },
        "applicable_directions": {
          "$ref": "#/definitions/ApplicableDirections"
        }
      },
      "required": [
        "track",
        "begin",
        "end",
        "applicable_directions"
      ]
    },
    "SpeedSection": {
      "title": "SpeedSection",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "speed_limit": {
          "title": "Speed Limit",
          "description": "Speed limit (m/s) applied by default to all trains",
          "type": "number"
        },
        "speed_limit_by_tag": {
          "title": "Speed Limit By Tag",
          "description": "Speed limit (m/s) applied to trains with a given tag",
          "type": "object",
          "additionalProperties": {
            "type": "number"
          }
        },
        "track_ranges": {
          "title": "Track Ranges",
          "type": "array",
          "items": {
            "$ref": "#/definitions/ApplicableDirectionsTrackRange"
          }
        }
      },
      "required": [
        "id",
        "speed_limit_by_tag",
        "track_ranges"
      ]
    },
    "Catenary": {
      "title": "Catenary",
      "type": "object",
      "properties": {
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "voltage": {
          "title": "Voltage",
          "type": "number"
        },
        "track_ranges": {
          "title": "Track Ranges",
          "type": "array",
          "items": {
            "$ref": "#/definitions/ApplicableDirectionsTrackRange"
          }
        }
      },
      "required": [
        "id",
        "voltage",
        "track_ranges"
      ]
    },
    "Side": {
      "title": "Side",
      "description": "An enumeration.",
      "enum": [
        "LEFT",
        "RIGHT",
        "CENTER"
      ],
      "type": "string"
    },
    "Signal": {
      "title": "Signal",
      "type": "object",
      "properties": {
        "track": {
          "$ref": "#/definitions/ObjectReference"
        },
        "position": {
          "title": "Position",
          "type": "number"
        },
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "direction": {
          "$ref": "#/definitions/Direction"
        },
        "sight_distance": {
          "title": "Sight Distance",
          "type": "number"
        },
        "linked_detector": {
          "$ref": "#/definitions/ObjectReference"
        },
        "aspects": {
          "title": "Aspects",
          "type": "array",
          "items": {
            "type": "string"
          }
        },
        "angle_sch": {
          "title": "Angle Sch",
          "description": "Schematic angle in degrees",
          "default": 0,
          "type": "number"
        },
        "angle_geo": {
          "title": "Angle Geo",
          "description": "Geographic angle in degrees",
          "default": 0,
          "type": "number"
        },
        "type_code": {
          "title": "Type Code",
          "type": "string"
        },
        "support_type": {
          "title": "Support Type",
          "type": "string"
        },
        "is_in_service": {
          "title": "Is In Service",
          "type": "boolean"
        },
        "is_lightable": {
          "title": "Is Lightable",
          "type": "boolean"
        },
        "is_operational": {
          "title": "Is Operational",
          "type": "boolean"
        },
        "comment": {
          "title": "Comment",
          "type": "string"
        },
        "physical_organization_group": {
          "title": "Physical Organization Group",
          "type": "string"
        },
        "responsible_group": {
          "title": "Responsible Group",
          "type": "string"
        },
        "label": {
          "title": "Label",
          "type": "string"
        },
        "installation_type": {
          "title": "Installation Type",
          "type": "string"
        },
        "value": {
          "title": "Value",
          "type": "string"
        },
        "side": {
          "description": "Side of the signal on the track",
          "default": "CENTER",
          "allOf": [
            {
              "$ref": "#/definitions/Side"
            }
          ]
        },
        "default_aspect": {
          "title": "Default Aspect",
          "description": "Aspect displayed when no train is around",
          "type": "string"
        }
      },
      "required": [
        "track",
        "position",
        "id",
        "direction",
        "sight_distance"
      ]
    },
    "BufferStop": {
      "title": "BufferStop",
      "type": "object",
      "properties": {
        "track": {
          "$ref": "#/definitions/ObjectReference"
        },
        "position": {
          "title": "Position",
          "type": "number"
        },
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "applicable_directions": {
          "$ref": "#/definitions/ApplicableDirections"
        }
      },
      "required": [
        "track",
        "position",
        "id",
        "applicable_directions"
      ]
    },
    "Detector": {
      "title": "Detector",
      "type": "object",
      "properties": {
        "track": {
          "$ref": "#/definitions/ObjectReference"
        },
        "position": {
          "title": "Position",
          "type": "number"
        },
        "id": {
          "title": "Id",
          "maxLength": 255,
          "type": "string"
        },
        "applicable_directions": {
          "$ref": "#/definitions/ApplicableDirections"
        }
      },
      "required": [
        "track",
        "position",
        "id",
        "applicable_directions"
      ]
    }
  }
}
;
    // Render toggable list in the container element
    document.getElementById("container").appendChild(
        renderjson(data)
    );
</script>

<style>
#container {
	text-shadow: none;
	background:;
	padding: 1em;
}

.renderjson a {
	text-decoration: none;
}

.renderjson .disclosure {
	color: #aa026d;
	font-size: 150%;
}

.renderjson .syntax {
	color: grey;
}

.renderjson .string {
	color: black;
}

.renderjson .number {
	color: cyan;
}

.renderjson .boolean {
	color: plum;
}

.renderjson .key {
	color: #aa026d;
}

.renderjson .keyword {
	color: lightgoldenrodyellow;
}

.renderjson .object.syntax {
	color: lightseagreen;
}

.renderjson .array.syntax {
	color: lightsalmon;
}
</style>
