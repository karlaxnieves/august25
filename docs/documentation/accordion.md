---
title: Accordion
deprecated: false
hidden: false
metadata:
  robots: index
---
Access Levels: | <i class="fa-solid fa-check" /> Community | <i class="fa-solid fa-check" /> Solo | <i class="fa-solid fa-check" /> Teams | <i class="fa-solid fa-check" /> Pro and Above

# Host Queries

Use these example queries to learn about the Censys Search Language and the searchable data available for hosts. For more information about search syntax, see Censys Query Language Syntax.

\<Accordion title="Censys Search Language Examples" icon="fa-info-circle">
&#x20; The table below provides working queries you can use to learn the Censys Search Language for querying hosts.

&#x20; The first column is the Censys Search Language showcased in the query. The second column describes the query. The third column is the query syntax linked to the Results page on search.censys.io.

&#x20; \<Table align=\{\["left","left","left","left"]}>
&#x20;   \<thead>
&#x20;     \<tr>
&#x20;       \<th style=\{\{ textAlign: "left" }}>
&#x20;         Search Type
&#x20;       \</th>

&#x20;       \<th style=\{\{ textAlign: "left" }}>
&#x20;         Description
&#x20;       \</th>

&#x20;       \<th style=\{\{ textAlign: "left" }}>
&#x20;         Link
&#x20;       \</th>

&#x20;       \<th style=\{\{ textAlign: "left" }}>
&#x20;         Query
&#x20;       \</th>
&#x20;     \</tr>
&#x20;   \</thead>

&#x20;   \<tbody>
&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Full Text Search
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         hello
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`hello\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Full Text Search
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts whose parsed data contains the words hello and world although not necessarily together
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`hello world\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Full Text Search
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts whose parsed data contains the phrase hello world
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`"hello world"\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Field:Value Pairs
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts with an HTTP service whose HTML title indicates it is exposing a directory
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`services.http.response.html\\\_title: "Index of /"\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Exact Match Operator
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts with an HTTP service whose hashed body content indicates that it is a Brute Ratel C4 server
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]\()
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         hello
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Boolean Logic
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts in the U.S.
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;          location.country=United States\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Set Operator
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts that have any of the following ports open
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`services.port: \{22, 23, 24, 25}\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Boolean Logic
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts that have no HTTP services
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`not services.service\\\_name: HTTP\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Boolean Logic
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts that have at least 1 non-HTTP service
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`services: (not\_service\_name: HTTP)\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Wildcards
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts with at least 1 service presenting a certificate during a TLS handshake
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`services.tls.certificate.fingerprint\_sha256: \*\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Regular Expressions

&#x20;         (Paid users only)
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts presenting certificates with a name&#x20;
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`services.tls.certificate.names=/foo\<1-100>.\*/\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Relative time
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts updated in the past hour
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`last\_updated\_at: \\\[now-1h TO now]\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Relative time
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for CVEs with a KEV added in the past 6 months
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`cves.kev.date\_added: \\\[now-6M TO now]\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Ranges
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts whose IP address falls within the specified range
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`ip: \\\[1.12.0.0 to 1.15.255.255]\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Ranges
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts whose location is within a box specified by its geographic coordinates

&#x20;         \> 📘 Tip  and open Search with the coordinate ranges populated.
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`and location.coordinates.longitude: \\\[34.16473388671876 to 34.58908081054688]\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Nested field queries
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts running the SSH protocol on ports other than 22 and 2222
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]\(
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`services:(service\\\_name: SSH and not (port: \{22, 2222}))\`
&#x20;       \</td>
&#x20;     \</tr>

&#x20;     \<tr>
&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Nested field queries
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         Search for hosts running Elasticsearch on port 443
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \[Try it]
&#x20;       \</td>

&#x20;       \<td style=\{\{ textAlign: "left" }}>
&#x20;         \`services: (service\\\_name: ELASTICSEARCH and port: 443)\`
&#x20;       \</td>
&#x20;     \</tr>
&#x20;   \</tbody>
&#x20; \</Table>
\</Accordion>

\<Accordion title="Host Attribute Examples" icon="fa-info-circle">
&#x20; The table provides working queries you can use to learn about the data model of hosts.

&#x20; The first column shows the top-level host attribute showcased in the query. The second column describes the query. The third column is the query syntax, linked to the Results page on search.censys.io.

&#x20; Some of these examples were gathered from \[community resources like this]\(https\://github.com/thehappydinoa/awesome-censys-queries)!

&#x20; \| Host Attribute                                    | Description                                                                                         | Link                                                                                                                                                                                                                                                                                                                                     | Query                                                                                                                                                |
&#x20; \| :------------------------------------------------ | :-------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------- |
&#x20; \| Perspective                                       | Search for hosts with services that were last observed by Censys Scanners within NTT and TELIA ISPs | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.perspective\_id%3A+%22PERSPECTIVE\_NTT%22+and+services.perspective\_id%3A+%22PERSPECTIVE\_TELIA%22)                                                                                                                 | \`services.perspective\\\_id: "PERSPECTIVE\\\_NTT" and services.perspective\\\_id: "PERSPECTIVE\\\_TELIA"\`                                                    |
&#x20; \| Web Servers                                       | Search for hosts with a page title on the HTTP service containing the word "dashboard"              | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.http.response.html\_title%3A+dashboard)                                                                                                                                                                          | \`services.http.response.html\\\_title: dashboard\`                                                                                                      |
&#x20; \| Web Servers                                       | Search for hosts that have an HTTP service that responded with a 500 status code                    | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.http.response.status\_code%3A+500)                                                                                                                                                                               | \`services.http.response.status\\\_code: 500\`                                                                                                           |
&#x20; \| Web Servers                                       | Search for hosts that have specific HTTP header value pairs                                         | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.http.response.headers.connection%3A+close+and+services.http.response.headers.content\_type%3A+%22text%2Fplain%22)                                                                                                | \`services.http.response.headers.connection: close and services.http.response.headers.content\\\_type: "text/plain"\`                                    |
&#x20; \| TLS                                               | Search for hosts that have an RDP service that is presenting a certificate                          | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services%3A+%28service\_name%3A+RDP+and+tls.certificate.fingerprint\_sha256%3A\*%29)                                                                                                                                        | \`services: (service\\\_name: RDP and tls.certificate.fingerprint\\\_sha256:\\\*)\`                                                                          |
&#x20; \| TLS                                               | Search for hosts with a service using TLSv1.0 encryption                                            | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.tls.version\_selected%3D%60TLSv1\_0%60)                                                                                                                                                                           | \`services.tls.version\\\_selected=TLSv1\\\_0\`                                                                                                            |
&#x20; \| TLS                                               | Search for hosts presenting a certificate with the string "localhost" in the subject\\\_dn            | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.tls.certificate.names%3A+localhost)                                                                                                                                                                             | \`services.tls.certificate.names: localhost\`                                                                                                          |
&#x20; \| Software                                          | Search for hosts running Microsoft IIS 7.5                                                          | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.software%3A+%28vendor%3A+Microsoft+and+product%3A+IIS+and+version%3A+7.5%29)                                                                                                                                    | \`services.software: (vendor: Microsoft and product: IIS and version: 7.5)\`                                                                           |
&#x20; \| Software with CPE URIs                            | Search for hosts running Microsoft Exchange                                                         | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.software.cpe%3A+%60cpe%3A2.3%3Aa%3Amicrosoft%3Aexchange\_server%3A\*%3A\*%3A\*%3A\*%3A\*%3A\*%3A\*%3A\*%60)                                                                                                              | \`services.software.cpe: cpe:2.3:a:microsoft:exchange\\\_server:\*:\*:\*:\*:\*:\*:\*:\*\`                                                                        |
&#x20; \| Searching CPE Software, OS, Product, Manufacturer | Search for hosts with a service running OpenSSH version 7.6p1 software on Linux version 18.04       | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services%3A+%28software.cpe%3A+%60cpe%3A2.3%3Ao%3Acanonical%3Aubuntu\_linux%3A18.04%3A\*%3A\*%3A\*%3A\*%3A\*%3A\*%3A\*%60+and+software.cpe%3A+%60cpe%3A2.3%3Aa%3Aopenbsd%3Aopenssh%3A7.6%3Ap1%3A\*%3A\*%3A\*%3A\*%3A\*%3A\*%3A\*%60%29) | \`services: (software.cpe: cpe:2.3:o:canonical:ubuntu\\\_linux:18.04:\*:\*:\*:\*:\*:\*:\\\* and software.cpe: cpe:2.3:a:openbsd:openssh:7.6:p1:\*:\*:\*:\*:\*:\*:\\\*)\` |
&#x20; \| Searching CPE Software, OS, Product, Manufacturer | Search for hosts running a Raspberry Pi product                                                     | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=services.software.product%3A+%22Raspberry+Pi%22)                                                                                                                                                                         | \`services.software.product: "Raspberry Pi"\`                                                                                                          |
&#x20; \| Searching Location                                | Search for hosts in Russia                                                                          | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=location.country%3A+Russia)                                                                                                                                                                                              | \`location.country: Russia\`                                                                                                                           |
&#x20; \| Search Location                                   | Search for hosts in Israel, excluding Tel Aviv.                                                     | \[Try it]\(https\://search.censys.io/search?resource=hosts\\\&sort=RELEVANCE\\\&per\_page=100\\\&virtual\_hosts=INCLUDE\\\&q=location.country\_code%3DIL+and+not+location.city%3A+%22Tel+Aviv%22)                                                                                                                                                      | \`location.country\\\_code=IL and not location.city: "Tel Aviv"\`                                                                                        |
\</Accordion>

# Certificate Queries

You can use Censys Search to identify expired or misconfigured SSL/TLS certificates and track vendor compliance. For more information about search syntax, see Censys Query Language Syntax.

See the video below for an overview of using search to identify expired or misconfigured certificates.

A tool currently in Beta leverages the natural-language processing of ChatGPT to produce valid query syntax in the Censys Search Language. Give it a try [here](https://gpt.censys.io/).

<Accordion title="Censys Query Language Examples" icon="fa-info-circle">
  The section below provides working queries you can use to learn the Censys Query Language for querying certificate records.

  The first column indicates the Censys Query Language feature showcased in the query. The second column describes the query. The third column shows the query syntax, which is linked to the Results page on search.censys.io.

  <Table align={["left","left","left"]}>
    <thead>
      <tr>
        <th style={{ textAlign: "left" }}>
          Search Type
        </th>

        <th style={{ textAlign: "left" }}>
          Description
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
          Search for cert records with any mention of the word apple anywhere.
        </td>

        <td style={{ textAlign: "left" }}>
          `apple`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Full Text Search
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records whose data contains the words apple and inc although not necessarily together
        </td>

        <td style={{ textAlign: "left" }}>
          `apple inc`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Full Text Search
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records whose data contains the phrase apple inc
        </td>

        <td style={{ textAlign: "left" }}>
          `"apple inc"`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Field:Value Pairs
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records whose name fields contain censys.io or any subdomain of that name
        </td>

        <td style={{ textAlign: "left" }}>
          `names: censys.io`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Exact Match Operator (`=`)
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records whose name fields contains the exact name censys.io
        </td>

        <td style={{ textAlign: "left" }}>
          `names=censys.io`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Boolean Logic
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records of unexpired but revoked certificates used for key agreement but not signing certificates
        </td>

        <td style={{ textAlign: "left" }}>
          `parsed.extensions.key\_usage.key\_agreement: true and parsed.extensions.key\_usage.certificate\_sign: false and labels=revoked and labels=unexpired`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Set Operator
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records that have any of the following validity lengths
        </td>

        <td style={{ textAlign: "left" }}>
          `parsed.validity_period.length_seconds: {`7.775999e+06, `7.862399e+06`, `3.1622399e+07`, `259199`}\`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Boolean Logic
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records whose certs were never trusted by NSS
        </td>

        <td style={{ textAlign: "left" }}>
          `not validation.nss.had\_trusted\_path: true`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Wildcards
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records with domain-style names that are similar to "censys"
        </td>

        <td style={{ textAlign: "left" }}>
          `names=cens?s.\*`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Regular Expressions

          (Paid users only)
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records with domain-style names that are similar to censys that use a certain TLD
        </td>

        <td style={{ textAlign: "left" }}>
          `names=/cens.\*s.(net\|info\|biz)/`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Relative time
        </td>

        <td style={{ textAlign: "left" }}>
          Search for certificates that were revoked in the last 8 hours
        </td>

        <td style={{ textAlign: "left" }}>
          `revocation.crl.revocation\_time: \[now-8h TO \*]`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Ranges
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records whose validity period ends between January 1 and January 30, 2024
        </td>

        <td style={{ textAlign: "left" }}>
          `parsed.validity\_period.not\_after: \[2024-01-01 to 2024-01-31]`
        </td>
      </tr>

      <tr>
        <td style={{ textAlign: "left" }}>
          Nested field queries
        </td>

        <td style={{ textAlign: "left" }}>
          Search for cert records entered into the Google Xenon 2024 CT log on October 30, 2023
        </td>

        <td style={{ textAlign: "left" }}>
          `ct.entries: (key=`google\_xenon\_2024` and value.added\_to\_ct\_at=`2023-10-30`)`
        </td>
      </tr>
    </tbody>
  </Table>
</Accordion>

<Accordion title="Certificate Attribute Examples" icon="fa-info-circle">
  The table provides working queries you can use to learn the data model of certificate records.

  The first column shows the type of information in the certificate record showcased in the query. The second column describes the query. The third column shows the query syntax, which is linked to the Results page on search.censys.io.

  | Cert Record Attribute    | Description                                                                                      | Query                                                             |
  | :----------------------- | :----------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
  | All Names                | Search for the name `[apple inc](censys.io)` in any of the names fields present in a cert record | `names=censys.io`                                                 |
  | All Names                | Search for the name `about.censys.io` in subject alternative name (SAN) field                    | `parsed.extensions.subject\_alt\_name.dns\_names=about.censys.io` |
  | Subject DN               | Search for cert records whose the subject DN includes an organization specified as "IBM"         | `parsed.subject.organization:”IBM”`                               |
  | Issuer DN                | Search for cert records of certs with a validity start and end date that are the same            | `parsed.issuer.common\_name="GTS X3"`                             |
  | Validity Period          | Search for cert records of certs with a validity start and end date that are the same            | `parsed.validity\_period.length\_seconds: 0`                      |
  | Certificate Transparency | Search for cert records not submitted to any CT log                                              | `not ct.entries: \*`                                              |
</Accordion>

<Accordion title="My Accordion Title" icon="fa-info-circle">
  Lorem ipsum dolor sit amet, **consectetur adipiscing elit.** Ut enim
  ad minim veniam, quis nostrud exercitation ullamco. Excepteur sint
  occaecat cupidatat non proident!

  <Accordion title="Certificate Attribute Examples" icon="fa-info-circle">
    The table provides working queries you can use to learn the data model of certificate records.

    The first column shows the type of information in the certificate record showcased in the query. The second column describes the query. The third column shows the query syntax, which is linked to the Results page on search.censys.io.

    | Cert Record Attribute    | Description                                                                                      | Query                                                             |
    | :----------------------- | :----------------------------------------------------------------------------------------------- | :---------------------------------------------------------------- |
    | All Names                | Search for the name `[apple inc](censys.io)` in any of the names fields present in a cert record | `names=censys.io`                                                 |
    | All Names                | Search for the name `about.censys.io` in subject alternative name (SAN) field                    | `parsed.extensions.subject\_alt\_name.dns\_names=about.censys.io` |
    | Subject DN               | Search for cert records whose the subject DN includes an organization specified as "IBM"         | `parsed.subject.organization:”IBM”`                               |
    | Issuer DN                | Search for cert records of certs with a validity start and end date that are the same            | `parsed.issuer.common\_name="GTS X3"`                             |
    | Validity Period          | Search for cert records of certs with a validity start and end date that are the same            | `parsed.validity\_period.length\_seconds: 0`                      |
    | Certificate Transparency | Search for cert records not submitted to any CT log                                              | `not ct.entries: \*`                                              |
  </Accordion>
</Accordion>