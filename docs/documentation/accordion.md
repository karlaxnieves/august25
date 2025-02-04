---
title: Accordion
deprecated: false
hidden: false
metadata:
  robots: index
---
<Accordion title="Censys Search Language Examples" icon="fa-info-circle">
  The table below provides working queries you can use to learn the Censys Search Language for querying hosts.

  The first column is the Censys Search Language showcased in the query. The second column describes the query. The third column is the query syntax linked to the Results page on search.censys.io.

  <Accordion title="Censys Search Language Examples" icon="fa-info-circle">
    <Table align={["left","left","left","left"]}>
      <thead>
        <tr>
          <th style={{ textAlign: "left" }}>
            Search Type
          </th>

          <th style={{ textAlign: "left" }}>
            Description
          </th>

          <th style={{ textAlign: "left" }}>
            Link
          </th>

          <th style={{ textAlign: "left" }}>
            Query
          </th>
        </tr>
      </thead>

      <tbody>
        <tr>
          <td style={{ textAlign: "left" }}>
            Full Text Search
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts whose parsed data contains the word hello
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=hello)
          </td>

          <td style={{ textAlign: "left" }}>
            `hello`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Full Text Search
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts whose parsed data contains the words hello and world although not necessarily together
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=hello+world)
          </td>

          <td style={{ textAlign: "left" }}>
            `hello world`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Full Text Search
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts whose parsed data contains the phrase hello world
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=%22hello+world%22)
          </td>

          <td style={{ textAlign: "left" }}>
            `"hello world"`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Field:Value Pairs
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts with an HTTP service whose HTML title indicates it is exposing a directory
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.http.response.html_title%3A+%22Index+of+%2F%22)
          </td>

          <td style={{ textAlign: "left" }}>
            `services.http.response.html\_title: "Index of /"`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Exact Match Operator
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts with an HTTP service whose hashed body content indicates that it is a Brute Ratel C4 server
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it]()
          </td>

          <td style={{ textAlign: "left" }}>
            `services.http.response.body\_hash="sha1:1a279f5df4103743b823ec2a6a08436fdf63fe30"`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Boolean Logic
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts in the U.S. with any reference to the string "teslamate"
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&virtual_hosts=INCLUDE\&q=%28teslamate%29+and+location.country%3D%60United+States%60)
          </td>

          <td style={{ textAlign: "left" }}>
            `(teslamate) and location.country=United States`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Set Operator
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts that have any of the following ports open: 22, 23, 24, 25
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.port%3A+%7B22%2C+23%2C+24%2C+25%7D)
          </td>

          <td style={{ textAlign: "left" }}>
            `services.port: {22, 23, 24, 25}`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Boolean Logic
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts that have no HTTP services
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=not+services.service_name%3A+HTTP+and+truncated%3A+false)
          </td>

          <td style={{ textAlign: "left" }}>
            `not services.service\_name: HTTP`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Boolean Logic
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts that have at least 1 non-HTTP service
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services%3A+%28not+service_name%3A+HTTP%29+and+truncated%3A+false)
          </td>

          <td style={{ textAlign: "left" }}>
            `services: (not_service_name: HTTP)`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Wildcards
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts with at least 1 service presenting a certificate during a TLS handshake
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.tls.certificate.fingerprint_sha256%3A+*)
          </td>

          <td style={{ textAlign: "left" }}>
            `services.tls.certificate.fingerprint_sha256: *`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Regular Expressions

            (Paid users only)
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts presenting certificates with a name foo1, foo2, foo3…foo100 followed by any value
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.tls.certificate.names%3D%2Ffoo%3C1-100%3E.*%2F)
          </td>

          <td style={{ textAlign: "left" }}>
            `services.tls.certificate.names=/foo<1-100>.*/`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Relative time
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts updated in the past hour
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=25\&virtual_hosts=EXCLUDE\&q=last_updated_at%3A+%5Bnow-1h+TO+*%5D)
          </td>

          <td style={{ textAlign: "left" }}>
            `last_updated_at: \[now-1h TO now]`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Relative time
          </td>

          <td style={{ textAlign: "left" }}>
            Search for CVEs with a KEV added in the past 6 months
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=25\&virtual_hosts=EXCLUDE\&q=cves.kev.date_added%3A+%5Bnow-6M+TO+*%5D)
          </td>

          <td style={{ textAlign: "left" }}>
            `cves.kev.date_added: \[now-6M TO now]`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Ranges
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts whose IP address falls within the specified range
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=ip%3A+%5B1.12.0.0+to+1.15.255.255%5D)
          </td>

          <td style={{ textAlign: "left" }}>
            `ip: \[1.12.0.0 to 1.15.255.255]`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Ranges
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts whose location is within a box specified by its geographic coordinates

            > 📘 Tip> [Draw a box on this map](https://workshop.censys.io/map-to-censys/)  and open Search with the coordinate ranges populated.
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=location.coordinates.latitude%3A+%5B31.2221970321032+to+31.596082850911525%5D+and+location.coordinates.longitude%3A+%5B34.16473388671876+to+34.58908081054688%5D)
          </td>

          <td style={{ textAlign: "left" }}>
            `location.coordinates.latitude: \[31.2221970321032 to 31.596082850911525] and location.coordinates.longitude: \[34.16473388671876 to 34.58908081054688]`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Nested field queries
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts running the SSH protocol on ports other than 22 and 2222
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services%3A%28service_name%3A+SSH+and+not+%28port%3A+%7B22%2C+2222%7D%29%29)
          </td>

          <td style={{ textAlign: "left" }}>
            `services:(service\_name: SSH and not (port: {22, 2222}))`
          </td>
        </tr>

        <tr>
          <td style={{ textAlign: "left" }}>
            Nested field queries
          </td>

          <td style={{ textAlign: "left" }}>
            Search for hosts running Elasticsearch on port 443
          </td>

          <td style={{ textAlign: "left" }}>
            [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services%3A+%28service_name%3A+ELASTICSEARCH+and+port%3A+443%29)
          </td>

          <td style={{ textAlign: "left" }}>
            `services: (service\_name: ELASTICSEARCH and port: 443)`
          </td>
        </tr>
      </tbody>
    </Table>
  </Accordion>
</Accordion>

<Accordion title="Host Attribute Examples" icon="fa-info-circle">
  The table provides working queries you can use to learn about the data model of hosts.

  The first column shows the top-level host attribute showcased in the query. The second column describes the query. The third column is the query syntax, linked to the Results page on search.censys.io.

  Some of these examples were gathered from [community resources like this](https://github.com/thehappydinoa/awesome-censys-queries)!

  | Host Attribute                                    | Description                                                                                         | Link                                                                                                                                                                                                                                                                                                                                     | Query                                                                                                                                                |
  | :------------------------------------------------ | :-------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
  | Perspective                                       | Search for hosts with services that were last observed by Censys Scanners within NTT and TELIA ISPs | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.perspective_id%3A+%22PERSPECTIVE_NTT%22+and+services.perspective_id%3A+%22PERSPECTIVE_TELIA%22)                                                                                                                 | `services.perspective\_id: "PERSPECTIVE\_NTT" and services.perspective\_id: "PERSPECTIVE\_TELIA"`                                                    |
  | Web Servers                                       | Search for hosts with a page title on the HTTP service containing the word "dashboard"              | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.http.response.html_title%3A+dashboard)                                                                                                                                                                          | `services.http.response.html\_title: dashboard`                                                                                                      |
  | Web Servers                                       | Search for hosts that have an HTTP service that responded with a 500 status code                    | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.http.response.status_code%3A+500)                                                                                                                                                                               | `services.http.response.status\_code: 500`                                                                                                           |
  | Web Servers                                       | Search for hosts that have specific HTTP header value pairs                                         | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.http.response.headers.connection%3A+close+and+services.http.response.headers.content_type%3A+%22text%2Fplain%22)                                                                                                | `services.http.response.headers.connection: close and services.http.response.headers.content\_type: "text/plain"`                                    |
  | TLS                                               | Search for hosts that have an RDP service that is presenting a certificate                          | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services%3A+%28service_name%3A+RDP+and+tls.certificate.fingerprint_sha256%3A*%29)                                                                                                                                        | `services: (service\_name: RDP and tls.certificate.fingerprint\_sha256:\*)`                                                                          |
  | TLS                                               | Search for hosts with a service using TLSv1.0 encryption                                            | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.tls.version_selected%3D%60TLSv1_0%60)                                                                                                                                                                           | `services.tls.version\_selected=TLSv1\_0`                                                                                                            |
  | TLS                                               | Search for hosts presenting a certificate with the string "localhost" in the subject\_dn            | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.tls.certificate.names%3A+localhost)                                                                                                                                                                             | `services.tls.certificate.names: localhost`                                                                                                          |
  | Software                                          | Search for hosts running Microsoft IIS 7.5                                                          | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.software%3A+%28vendor%3A+Microsoft+and+product%3A+IIS+and+version%3A+7.5%29)                                                                                                                                    | `services.software: (vendor: Microsoft and product: IIS and version: 7.5)`                                                                           |
  | Software with CPE URIs                            | Search for hosts running Microsoft Exchange                                                         | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.software.cpe%3A+%60cpe%3A2.3%3Aa%3Amicrosoft%3Aexchange_server%3A*%3A*%3A*%3A*%3A*%3A*%3A*%3A*%60)                                                                                                              | `services.software.cpe: cpe:2.3:a:microsoft:exchange\_server:*:*:*:*:*:*:*:*`                                                                        |
  | Searching CPE Software, OS, Product, Manufacturer | Search for hosts with a service running OpenSSH version 7.6p1 software on Linux version 18.04       | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services%3A+%28software.cpe%3A+%60cpe%3A2.3%3Ao%3Acanonical%3Aubuntu_linux%3A18.04%3A*%3A*%3A*%3A*%3A*%3A*%3A*%60+and+software.cpe%3A+%60cpe%3A2.3%3Aa%3Aopenbsd%3Aopenssh%3A7.6%3Ap1%3A*%3A*%3A*%3A*%3A*%3A*%3A*%60%29) | `services: (software.cpe: cpe:2.3:o:canonical:ubuntu\_linux:18.04:*:*:*:*:*:*:\* and software.cpe: cpe:2.3:a:openbsd:openssh:7.6:p1:*:*:*:*:*:*:\*)` |
  | Searching CPE Software, OS, Product, Manufacturer | Search for hosts running a Raspberry Pi product                                                     | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=services.software.product%3A+%22Raspberry+Pi%22)                                                                                                                                                                         | `services.software.product: "Raspberry Pi"`                                                                                                          |
  | Searching Location                                | Search for hosts in Russia                                                                          | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=location.country%3A+Russia)                                                                                                                                                                                              | `location.country: Russia`                                                                                                                           |
  | Search Location                                   | Search for hosts in Israel, excluding Tel Aviv.                                                     | [Try it](https://search.censys.io/search?resource=hosts\&sort=RELEVANCE\&per_page=100\&virtual_hosts=INCLUDE\&q=location.country_code%3DIL+and+not+location.city%3A+%22Tel+Aviv%22)                                                                                                                                                      | `location.country\_code=IL and not location.city: "Tel Aviv"`                                                                                        |
</Accordion>

<Accordion title="Hosts" icon="fa-info-circle">
  Hosts are computers, virtual machines, or devices with an IP address connected to the Internet. Host fields include those that apply to the whole host (such as geolocation or Internet routing) and those that apply to services observed on open ports.

  ###

  <Accordion title="Host, host.operating_system" icon="fa-info-circle" />
</Accordion>