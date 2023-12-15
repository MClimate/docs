# 📖 Vicki LoRaWAN Device communication protocol

## Foreword

In the current section, we explain in detail what are the specific commands that the device supports.&#x20;

If you want to make yourself familiar with the details of how this device operates, please read through all articles.

## Communication concepts related to LoRaWAN standard

* Supported LoRaWAN MAC protocol version: 1.0.3;
* Supported LoRaWAN device class: A;
* LoRaWAN MAC Port:&#x20;
  * Uplinks: 2.&#x20;
  * **Downlinks: 1, 2, 4-223;**
* Maximum application payload size: Maximum allowed by document “LoRaWAN regional parameters” for DataRate 0 for the given region. In most of the cases this is 51 bytes;
* Consult the document “LoRaWAN regional parameters” for additional technical information (Especially for RX2 window timings);

## Release notes

{% hint style="info" %}
Release notes for the different firmware versions of Vicki are available [here](./#undefined).
{% endhint %}

## Document versions history

<table data-header-hidden><thead><tr><th width="186.73211781206172">Date</th><th width="150">Version</th><th width="163">Author</th><th>Comment</th></tr></thead><tbody><tr><td><strong>Date</strong></td><td><strong>Version</strong></td><td><strong>Author</strong></td><td><strong>Comment</strong></td></tr><tr><td>7 May 2020</td><td>V1.0</td><td>Martin Peevski</td><td>Initial draft</td></tr><tr><td>8 May 2020</td><td>V1.1</td><td>Milan Stefanov &#x26; Lyubomir Yanchev</td><td><p>Document review;</p><p>Message examples inclusion.</p></td></tr><tr><td>20 May 2020</td><td>V1.2</td><td>Martin Peevski</td><td>Added general information and more supported commands.</td></tr><tr><td>20 May 2020</td><td>V1.3</td><td>Milan Stefanov &#x26; Lyubomir Yanchev</td><td>Document review and visual edits.</td></tr><tr><td>27 May 2020</td><td>V1.4</td><td>Lyubomir Yanchev</td><td>Document general formatting.</td></tr><tr><td>15 June 2020</td><td>V1.5</td><td>Martin Peevski</td><td>All chapters updated; Added support to read all commands parameters (GET commands).</td></tr><tr><td>11 August 2020</td><td>V1.6</td><td>Martin Peevski</td><td><p>Chapters updated:</p><ul><li><a href="communication-concepts.md#communication-concepts-related-to-lorawan-standard">Communication concepts related to LoRaWAN standard</a></li><li><a href="keep-alive.md#set-keep-alive-period-command-explanation">Keep-alive period set command explanation</a></li><li><a href="uplink-types.md#set-uplink-messages-type-command-explanation">Set uplink messages type command explanation</a></li></ul><p>Added new commands </p><ul><li><a href="network-related-settings.md#set-device-radio-communication-watch-dog-parameters-command-explanation">Set WDP parameters</a></li><li><a href="network-related-settings.md#get-device-radio-communication-watch-dog-parameters-command-explanation">Get WDP parameters</a></li></ul></td></tr><tr><td>28 September 2020</td><td>V1.7</td><td>Martin Peevski</td><td><p>Updated chapters </p><ul><li><a href="operational-modes-and-temperature-control-algorithm/#set-internal-temperature-control-algorithm-parameters">Set internal temperature control algorithm parameters</a></li><li><a href="operational-modes-and-temperature-control-algorithm/#set-internal-temperature-control-algorithm-parameters-tdiff-only">Set internal temperature control algorithm parameters – Tdiff only</a></li><li><a href="operational-modes-and-temperature-control-algorithm/#get-internal-temperature-control-algorithm-parameters">Get internal temperature control algorithm parameters</a></li><li><a href="operational-modes-and-temperature-control-algorithm/#get-internal-temperature-control-algorithm-parameters-tdiff-only">Get internal temperature control algorithm parameters – Tdiff only</a></li></ul><p>Added new commands </p><ul><li><a href="operational-modes-and-temperature-control-algorithm/#set-device-primary-operational-mode">Set device primary operational mode</a></li><li><a href="operational-modes-and-temperature-control-algorithm/#get-device-primary-operational-mode">Get device primary operational mode</a></li></ul></td></tr><tr><td>15 December 2021</td><td>Version notes deprecated</td><td>Lyubomir Yanchev</td><td>We've decided to switch to a cleaner view of the release notes and separate them in a special page. <a href="../release-notes.md">See the Release notes here.</a></td></tr></tbody></table>
