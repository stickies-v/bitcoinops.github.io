---
title: 'Bitcoin Optech Newsletter #385: 2025 Year-in-Review Special'
permalink: /en/newsletters/2025/12/19/
name: 2025-12-19-newsletter
slug: 2025-12-19-newsletter
type: newsletter
layout: newsletter
lang: en

excerpt: >
  The eighth annual Bitcoin Optech Year-in-Review special summarizes notable
  developments in Bitcoin during all of 2025.
---

{{page.excerpt}} It's the sequel to our summaries from [2018][yirs 2018],
[2019][yirs 2019], [2020][yirs 2020], [2021][yirs 2021], [2022][yirs 2022],
[2023][yirs 2023], and [2024][yirs 2024].

## Contents

* January
  * [Updated ChillDKG draft](#chilldkg)
  * [Offchain DLCs](#offchaindlcs)
  * [Stats on compact block reconstruction](#compactblockstats)
* February
  * [Erlay update](#erlay)
  * [LN ephemeral anchor scripts](#lneas)
  * [Probabilistic payments](#probpayments)
* March
  * [Bitcoin Forking Guide](#forkingguide)
  * [Private block template marketplace to prevent centralizing MEV](#templatemarketplace)
  * [LN upfront and hold fees using burnable outputs](#lnupfrontfees)
* April
  * [SwiftSync speedup for initial block download](#swiftsync)
  * [DahLIAS interactive aggregate signatures](#dahlias)
* May
  * [Cluster mempool](#clustermempool)
  * [Increasing or removing Bitcoin Core’s OP_RETURN size limit](#opreturn)
* June
  * [Calculating the selfish mining danger threshold](#selfishmining)
  * [Fingerprinting nodes using addr messages](#fingerprinting)
  * [Garbled locks](#garbledlocks)
* July
  * [Chain code delegation](#ccdelegation)
* August
  * [Utreexo draft BIPs](#utreexo)
  * [Lowering the minimum relay feerate](#minfeerate)
  * [Peer block template sharing](#templatesharing)
  * [Differential fuzzing of Bitcoin and LN implementations](#fuzzing)
* September
  * [Details about the design of Simplicity](#simplicity)
  * [Partitioning and eclipse attacks using BGP interception](#eclipseattacks)
* October
  * [Theoretical limitations on embedding data in the UTXO set](#arbdata)
  * [Channel jamming mitigation simulation results and updates](#channeljamming)
* November
  * [Comparing performance of ECDSA signature validation in OpenSSL vs. libsecp256k1](#secpperformance)
  * [Multiple discussions about restricting data](#restrictingdata)
  * [Modeling stale rates by propagation delay and mining centralization](#stalerates)
  * [BIP3 and the BIP process](#bip3)
  * [Bitcoin Kernel C API introduced](#kernelapi)
* December
* Featured summaries
  * [Vulnerabilities](#vulns)
  * [Quantum](#quantum)
  * [Soft fork proposals](#softforks)
  * [Stratum V2](#stratumv2)
  * [Major releases of popular infrastructure projects](#releases)
  * [Bitcoin Optech](#optech)

---

## January

{:#chilldkg}
- **Updated ChillDKG draft:** Tim Ruffing and Jonas Nick updated their work on
  a distributed key generation protocol (DKG) for use with the [FROST][news
  frost bip] [threshold signature][topic threshold signature] scheme. ChillDKG
  aims to provide similar recoverability features to existing descriptor
  wallets.

{:#offchaindlcs}
- **Offchain DLCs:** Developer Conduition [posted about][news offchain dlc] a
  new offchain DLC ([discreet log contract][topic dlc]) mechanism that enables
  participants to collaborate on the creation and extension of a DLC factory
  which allows iterative DLCs that roll along until one party chooses to
  resolve on chain. This contrasts with [prior work][news dlc channels] on
  offchain DLCs which required interaction at each roll of the contract.

{:#compactblockstats}
- **Stats on compact block reconstruction:** ...

## February

{:#erlay}
- **Erlay update:** Sergi Delgado made [several posts][erlay optech posts] over
  the last year about his work and progress implementing [Erlay][erlay] for
  Bitcoin Core. In the first post, he gave an overview on the Erlay proposal and
  how the current transaction relay works (called fanout). In these posts, he
  discusses different results that he found while developing Erlay, such as
  [filtering based on transaction knowledge][erlay knowledge] not mattering as
  much as expected. He also experimented with selecting [how many peers should
  receive a fanout][erlay fanout amount], and found that there was a 35%
  bandwidth savings with 8 outbound peers and 45% with 12 outbound peers, but
  also found a 240% increase in latency. In his two other experiments, he
  determined the [fanout rate based on how a transaction was
  received][erlay transaction received] and [when to select canidate
  peers][erlay candidate peers]. These experiments, which combined fanout and
  reconciliation, helped him determine when to use each method.

{:#lneas}
- **LN ephemeral anchor scripts:** ...

{:#probpayments}
- **Probabilistic payments:** ...

<div markdown="1" class="callout" id="vulns">

## Summary 2025: Vulnerabilities

...

</div>

## March

{:#forkingguide}
- **Bitcoin Forking Guide:** Anthony Towns [posted][fork guide post] to Delving
  Bitcoin a guide on how to build community consensus for changes to Bitcoin’s
  consensus rules. According to Towns, the process of establishing consensus can
  be divided in four steps, namely [research and development][fork guide red],
  [power user exploration][fork guide pue], [industry evaluation][fork guide
  ie], and [investor review][fork guide ir]. However, Towns warned readers that
  the guide aims to be only a high-level procedure, and that it could work only
  in a cooperative environment.

{:#templatemarketplace}
- **Private block template marketplace to prevent centralizing MEV:** Developers
  Matt Corallo and 7d5x9 [posted][template mrkt post] to Delving Bitcoin a
  proposal that would allow to prevent a future in which MEVil — a form of MEV
  extraction leading to mining centralization — proliferates on Bitcoin. The
  proposal, referred to as [MEVpool][mevpool gh], would allow parties to bid in
  public markets for selected space within miner block templates (i.e. "I’ll pay
  X [BTC] to include transaction Y as long as it comes before any other
  transaction which interacts with the smart contract identified by Z").

  While today services of preferential transaction ordering within block
  templates are expected to be provided only by large miners, leading to
  centralization, a trust-reduced public market would allow any miner to work on
  blinded block templates whose complete transactions aren’t revealed to miners
  until they’ve produced sufficient proof of work to publish the block.

  The authors warned that this proposal would require multiple marketplaces to
  compete to help preserve decentralization against the dominance of a single
  trusted marketplace.

{:#lnupfrontfees}
- **LN upfront and hold fees using burnable outputs:** John Law [posted][ln fees post]
  to Delving Bitcoin the summary of a [paper][ln fees paper] he has written about a
  protocol that Lighting nodes can use to charge two additional types of fees for
  forwarding payments, an upfront fee and a hold fee. The former would be paid by
  the ultimate spender to compensate forwarding nodes for temporarily using an
  [HTLC][topic htlc] slot, while the latter would be paid by any node that delays
  the settlement of an HTLC, with the payment amount scaling up with the length
  of the delay.

  Law describes the protocol as a solution for
  [channel jamming attacks][topic channel jamming attacks], a weakness in the Lightning
  Network protocol that allows an attacker to costlessly prevent other nodes
  from using some or all of their funds.

## April

{:#swiftsync}
- **SwiftSync speedup for initial block download:** Sebastian Falbesoner
  [posted][swiftsync delving post] to Delving Bitcoin a sample implementation
  and results of a >5x speedup of _initial block download_ (IBD) through
  SwiftSync, an idea initially [proposed][swiftsync ruben gh] by Ruben Somsen.

  The speedup is achieved during IBD by only adding coins to the UTXO set when
  they will still be in the UTXO set at the end of IBD. This knowledge of the
  final UTXO set state stated is compactly encoded in a minimally trusted
  pre-generated hints file. In addition to minimizing overhead on chainstate
  operations, SwiftSync enables further performance improvements by allowing
  parallel block validation.

  Work on a Rust implementation is [underway][swiftsync rust impl].


{:#dahlias}
- **DahLIAS interactive aggregate signatures:** Jonas Nick, Tim Ruffing, Yannick
  Seurin [posted][dahlias post] to the Bitcoin-Dev mailing list to announce a
  [paper][dahlias paper] they’ve written about DahLIAS, the first interactive
  64-byte aggregate signature scheme compatible with the cryptographic
  primitives already used by Bitcoin, called secp256k1. Aggregate signatures are
  the cryptographic requirement for [cross-input signature aggregation][topic
  cisa] (CISA), a feature proposed for Bitcoin that could reduce the size of
  transactions with multiple inputs, thus reducing the cost of many different
  types of spending, [coinjoins][topic coinjoin] and [payjoins][topic payjoin]
  included.

<div markdown="1" class="callout" id="quantum">

## Summary 2025: Quantum

TODO: intro / non consensus discussions?...

{:quantumforks}
- **Quantum mitigation consensus proposals**: With the increase in attention
  on the potential for a future quantum computer to weaken or break the
  Elliptic Curve Discrete Logarithm (ECDL) hardness assumption that Bitcoin
  relies on to prove the ownership of coins, quite a few proposals were put
  forward to mitigate the impact of such a development.

  Two proposals ([1][news qr sha], [2][news qr cr]) were made to enable
  most existing coins to be secured in a way that could be recovered in the
  event that bitcoin disables quantum vulnerable spends at some later point.
  Briefly, the theorized sequence of events is 0) Bitcoin holders ensure that
  their current wallets have some hashed secret required for some spend path
  1) a cryptographically relevant quantum computer (CRQC) is shown to be
  eminent, 2) Bitcoin disables elliptic curve signatures, 3) Bitcoin enables a
  quantum secure signature scheme, 4) Bitcoin enables one of these proposals
  enabling prepared holders to claim their quantum vulnerable coins. Depending
  on the exact implementation, any address type (including P2TR with any
  script path) could take advantage of these methods.

  Augustin Cruz [proposed][news qr cruz] a [BIP][qr bip destroy] to destroy
  definitely quantum vulnerable coins. Subsequently, Jameson Lopp [started a
  discussion][news qr lopp1] of how quantum vulnerable coins should be handled
  which led to several ideas ranging from letting the quantum adversary have
  them to destroying them. Lopp later [proposed][news qr lopp2] a concrete
  sequence of soft forks that Bitcoin could implement beginning long before a
  CRQC is developed to gradually mitigate the threat of a quantum adversary
  suddenly gaining access to many coins while allowing holders time to secure
  their coins.

  [BIP360][BIPs #1895] was [updated][news bip360 update] and received its BIP
  number. The updated proposal is now referred to as P2TRH (pay to taproot
  hash) instead of the earlier name P2QRH (pay to quantum resistant hash),
  reflecting its reduced scope and increased generality. This proposal has
  garnered widespread support both as a first step toward quantum hardening
  bitcoin and an optimization for taproot use cases that do not require an
  internal key.

  Developer Conduition demonstrated that [`OP_CAT`][BIP347] can be used to
  implement Winternitz signatures, which provides a quantum resistant
  signature check at a cost of ~2000 vBytes per input. This is less costly
  than the previously [proposed][rubin lamport] `OP_CAT`-based [Lamport
  signatures][lamport].

  Matt Corallo started a [discussion][news qr corallo] around the general idea
  of adding a quantum resistant signature checking opcode to tapscript. Later,
  Abdelhamid Bakhta [proposed][abdel stark] native STARK verification as one
  such opcode and Conduition [wrote][conduition sphincs] about their work
  optimizing SLH-DSA (SPHINCS) quantum resistant signatures as another option.

  Any quantum resistant signature checking opcode including `OP_CAT` added to
  tapscript could be combined with [BIP360][] to fully quantum harden Bitcoin
  outputs.

  Tadge Dryja [proposed][news qr agg] one way in which bitcoin could implement
  general cross-input signature aggregation which would partially mitigate the
  large size of post-quantum signatures.

</div>

## May

{:#clustermempool}
- **Cluster mempool:**
  In January, Stefan Richter prompted excitement by [discovering][news340 richter ggt]
  that an efficient algorithm for the _maximum-ratio closure problem_ from a
  1989 research paper could be applied to cluster linearization. Pieter Wuille
  extended his research to incorporate this minimal-cut-based third approach.
  In February, Pieter Wuille [walked][news341 pr-review-club txgraph] the Bitcoin Core
  PR Review Club through the newly introduced `TxGraph` class which distills
  transactions to only weight, fees, and relationships for efficient
  interaction with the mempool graph.
  In May, Wuille described the [tradeoffs][news352 wuille linearization techniques] of
  the three cluster linearization approaches and provided benchmarks, finding
  that both advanced approaches were far more efficient than the simple
  candidate-set search, but the linear programming-based spanning-forest
  linearization algorithm would be more practical than the min-cut-based
  algorithm.
  In October, Abubakar Sadiq Ismail [described][news377 ismail
  template improvement] how the cluster mempool could be leveraged to track
  when the mempool content had significantly improved upon a prior block
  template.
  In November, the cluster mempool implementation was [completed][news382 cluster
  mempool completed], staging it to be released per Bitcoin
  Core 31.0. Work to replace the initial candidate-set search linearization
  algorithm with the spanning-forest linearization algorithm is on-going.

{:#opreturn}
- **Increasing or removing Bitcoin Core’s OP_RETURN size limit:** ...

## June

{:#selfishmining}
- **Calculating the selfish mining danger threshold:** Antoine Poinsot
  [posted][selfish miner post] to Delving Bitcoin an expansion of the math from
  the 2013 [paper][selfish miner paper] that gave the [selfish mining
  attack][topic selfish mining] its name. Poinsot focused on reproducing one of
  the conclusions of the paper, proving that a dishonest miner controlling 33%
  of the total network hashrate, with no additional advantages, can become
  marginally more profitable on a long term basis than the miners controlling
  67% of it.

{:#fingerprinting}
- **Fingerprinting nodes using addr messages:** Daniela Brozzoni
  [posted][fingerprinting post] to Delving Bitcoin about research she conducted,
  together with developer Naiyoma, into identifying the same node on multiple
  networks using the `addr` messages, which are sent by the nodes, through the
  P2P protocol, to advertise other potential peers. Brozzoni and Naiyoma were
  able to fingerprint individual nodes using details from their specific address
  messages, allowing them to identify the same node running on multiple networks
  (such as IPv4 and [Tor][topic anonymity networks]). Researchers suggested two
  possible mitigations, either removing timestamps from address messages or, if
  the timestamps are kept, randomizing them slightly to make them less specific
  to particular nodes.

{:#garbledlocks}
- **Garbled locks:** Robin Linus [posted][bitvm3 post] to Delving Bitcoin to
  announce a significant reduction in the amount of onchain space required by
  [BitVM][topic acc]-style contracts. Based on an [idea][delbrag rubin] by
  Jeremy Rubin, the new approach leverages [Garbled Circuits][garbled circuits
  wiki], a cryptographic primitive that makes onchain SNARK verification a
  thousand times more efficient than the BitVM2 implementation, at the cost of
  requiring a multi-terabyte offchain setup.

  On the same topic, Liam Eagen [posted][eagen ml] to the Bitcoin-Dev mailing
  list about a [paper][eagen paper] he has written about a new mechanism for
  creating [accountable computing contracts][topic acc] based on Garbled
  Circuits, called Glock (Garbled Locks). While the approach is similar, Eagen's
  research is independent from Linus'. According to Eagen, Glock allows for a
  550x reduction of onchain data compared to BitVM2.

<div markdown="1" class="callout" id="softforks">

## Summary 2025: Soft fork proposals

This year saw a bevvy of discussions around soft fork proposals ranging from
the tightly scoped and minimally impactful, to the broadly scoped and
powerful, to the significantly confiscatory.

{:#txtemplates}
- **Transaction Templates:** Several soft fork packages were discussed around
  transaction templates. With similar scope and capability are CTV+CSFS
  ([BIP119][]+[BIP348][]) and the [taproot-native re-bindable signature
  package][news thikcs] ([`OP_TEMPLATEHASH`][BIPs
  #1974]+[BIP348][]+[BIP349][]). These represent the minimal capability
  enhancement for Bitcoin Script to enable both re-bindable signatures
  (signatures that do not commit to spending a specific UTXO), and
  pre-commitment to spending a UTXO to a specific next transaction (sometimes
  called an equality covenant). If activated, they would enable
  LN-Symmetry][ctv csfs symmetry], [simple CTV vaults][ctv vaults], [reduce DLC
  signature requirements][ctv dlcs], [reduce interactivity for Arks][ctv
  csfs arks], [simplify PTLCs][ctv csfs ptlcs], and more. One difference
  between these proposals is that `OP_TEMPLATEHASH` cannot be used in the
  [BitVM sibling hack][ctv csfs bitvm] where CTV can, due to `OP_TEMPLATEHASH`
  not committing to `scriptSigs`.

  By including CSFS, these proposals also enable multi-commitments (committing
  to multiple related and optionally ordered values in a locking or spend
  script) similar to merkle trees through [Key Laddering][rubin key ladder].
  The updated [LNHANCE][lnhance update] proposal includes `OP_PAIRCOMMIT`
  ([BIPs #1699][]) to enable multi-commitments without the additional script
  size and validation cost required for Key Laddering. Multi-commitments are
  useful in LN-Symmetry, complex delegations, and more.

  Some developers [expressed frustration][ctv csfs letter] about the (from
  their perspective) slow progress toward a soft fork, but the volume of
  discussion around this category of proposal suggests that interest and
  enthusiasm remain high.

{:#consensuscleanup}
- **Consensus Cleanup:** The [consensus cleanup][topic consensus cleanup] proposal
  was [updated][gcc update] based on feedback and additional research, a
  [draft bip][gcc bip] was published and merged as [BIP54][] and now [includes
  an implementation and test vectors][gcc impl tests]. Earlier this year,
  there was [discussion][transitory cleanups] of whether such cleanups should
  be made temporary in case of unintentional confiscation, but the necessity
  of reevaluating such a [temporary soft fork][topic transitory soft forks] to avoid a chain split every time
  it expires makes such temporary soft forks a hard sell.

{:opcodes}
- **Opcode proposals:** In addition to the grouped changes discussed above,
  there were a number of other Script opcodes proposed or refined in 2025.

  `OP_CHECKCONTRACTVERIFY` (CCV) [became][ccv bip] [BIP443][] with
  [refined][ccv semantics] semantics especially around flow of funds. CCV
  enables reactive security vaults, and a wide array of other contracts by
  constraining the `scriptPubKey` and amount of an input or output in certain
  ways. The `OP_VAULT` proposal was [withdrawn][vault withdrawn] in favor of
  CCV as well. For more on CCV's applications, see [MATT][topic MATT].

  A set of 64-bit arithmetic opcodes were [proposed][64bit bip]. Bitcoin's
  current math operations are (surprisingly) not able to operate on the full
  range of Bitcoin input and output amounts. Combined with other opcodes to
  access and/or constrain input/output amounts, these expanded arithmetic
  operations could enable new Bitcoin wallet functionality.

  A [variant][txhash sponsors] of [`OP_TXHASH`][txhash] would enable
  [transaction sponsorship][topic fee sponsorship].

  Developers proposed two options for giving Script elliptic curve
  cryptographic operations other than `OP_CHECKSIG` and related operations. One
  [proposes][tweakadd] `OP_TWEAKADD` to enable constructing taproot
  `scriptPubKeys`. The other [proposes][ecmath] more granular elliptic curve
  opcodes such as `EC_POINT_ADD` motivated by similar functionality, but with
  more potential applications such as new signature verifications or multi-signature
  functionality. Either of these proposals could be combined with `OP_TXHASH`
  and 64-bit arithmetic (or similar opcodes) to enable functionality similar
  to CCV.

{:scriptrestoration}
- **Script Restoration:** A series of 4 BIPs were [posted][gsr bips] for the
  Script Restoration project. The Script changes and opcodes proposed in these
  4 BIPs would enable all of the functionality proposed in the above opcode
  proposals while allowing even more script expressivity.

</div>

## July

{:#ccdelegation}
- **Chain code delegation:** ...

## August

{:#utreexo}
- **Utreexo draft BIPs:** ...

{:#minfeerate}
- **Lowering the minimum relay feerate:** ...

{:#templatesharing}
- **Peer block template sharing:** ...

{:#fuzzing}
- **Differential fuzzing of Bitcoin and LN implementations:** ...

## September

{:#simplicity}
- **Details about the design of Simplicity:** After the release of
  [Simplicity][topic simplicity], Russel O'Connor made three posts to
  Delving Bitcoin to discuss the [philosophy and the design][simplicity 370] behind the
  language:
  - [Part I][simplicity I post]: It examines the three major forms of composition
    for transforming basic operations into complex ones.
  - [Part II][simplicity II post]: It dives into Simplicity’s type system
    combinators, and basic expressions.
  - [Part III][simplicity III post]: It explains how to build logical operations
    starting from bits up to cryptographic operations using just computational
    Simplicity combinators.

  Since September, two more posts have been published to Delving Bitcoin,
  [Part IV][simplicity IV post], discussing about side effects, and
  [Part V][simplicity V post], dealing with programs and addresses.

{:#eclipseattacks}

- **Partitioning and eclipse attacks using BGP interception:** Cedarctic
  [posted][Cedarctic post] to Delving Bitcoin about flaws in Border Gateway
  Protocol (BGP) to prevent full nodes from being able to connect to peers,
  which could be used to partition the network or execute an [eclipse
  attack][eclipse attack]. Several mitigations were described by cedarctic,
  with other developers in the discussion describing other mitigations and
  ways to monitor for use of the attack.

<div markdown="1" class="callout" id="stratumv2">

## Summary 2025: Stratum V2

[Stratum V2][topic pooled mining] is a mining protocol designed to replace the
original Stratum protocol used between miners and mining pools. One of its key
advantages is that it can allow individual pool members to choose which
transactions to include in their blocks. This could improve Bitcoin's censorship
resistance by distributing transaction selection across many independent miners.

Throughout 2025, Bitcoin Core received several updates to better support Stratum
V2 implementations. Some improvements earlier in the year were focused on
improving the mining RPCs, [upgrading them][news339 sv2fields] with `nBits`,
`target`, and `next` fields, useful for constructing and validating block
templates.

The most significant work focused on Bitcoin Core's experimental inter-process
communication (IPC) interface, which allows an external Stratum V2 service to
interact with Bitcoin Core's block validation without going through the slower
JSON-RPC interface. A new [`waitNext()`][news346 waitnext] method was introduced
to the `BlockTemplate` interface that only returns a new template when the chain
tip changes or when mempool fees increase significantly, reducing unnecessary
template generation. [`checkBlock`][news360 checkblock] was then added, enabling
pools to validate miner-provided templates via IPC. IPC was also
[enabled][news369 ipc] by default, and the new `bitcoin-node` and other
multiprocess binaries added to release builds. A new bitcoin wrapper executable
was [added][Bitcoin Core #31375] to easily discover and launch an increasing number
of binaries, and a follow-up [implemented][news374 ipcauto] automatic
multiprocess selection, removing the need for the `-m` startup flag. This year's
IPC improvements were wrapped up by [reducing CPU consumption][news377 ipclog]
for multiprocess logging and [ensuring][news381 witness] that blocks submitted
via IPC have their witness commitment revalidated.

[Bitcoin Core 30.0][news376 30], released in October, was the first release to
include the experimental IPC mining interface after it was first
[introduced][news323 miningipc] last year.

In June, StarkWare [demonstrated][news359 starkware] a modified Stratum v2
client using STARK proofs to prove that a block's fees belong to a valid
template without revealing the block's transactions. Two new Stratum V2-based
mining pools also launched: [Hashpool][news346 hashpool], which represents
mining shares as [ecash][topic ecash] tokens, and DMND, which expanded from solo
mining to pooled mining.

</div>

<div markdown="1" class="callout" id="releases">

## Summary 2025: Major releases of popular infrastructure projects

FIXME:Gustavojfe

</div>

## October

{:#arbdata}
- **Theoretical limitations on embedding data in the UTXO set:** ...

{:#channeljamming}
- **Channel jamming mitigation simulation results and updates:** Carla
  Kirck-Cohen in collaboration with Clara Shikhelman and elnosh had updated the
  [lightning jamming simulation results][channel jamming results], and updates
  to their reputation algorithm. The updates included reputation tracking for
  outgoing channels, and resources being limited on incoming channels. With
  these new updates, they found that it still protects against
  [resource][channel jamming resource] and [sink][channel jamming sink] attacks.
  After this round of updates and simulations, they feel that [channel jamming
  attack][channel jamming attack] mitigation has reached a point where it is
  good enough.

## November

{:#secpperformance}
- **Comparing performance of ECDSA signature validation in OpenSSL vs. libsecp256k1:** Sebastian Falbesoner conducted an
  [analysis][openssl vs libsecp256k1] on the performance of ECDSA signature
  validation between OpenSSL and libsecp256k1. Since 2015, Bitcoin Core has used
  libsecp256k1 over OpenSSL. He wanted to be certain that doing so was the right
  choice and not a wasted effort. From the start, libsecp256k1 was 2.5-5.5 times
  faster than OpenSSL, but this analysis was done to see if OpenSSL had made any
  improvements over the decade and if so did libsecp256k1 keep up. What
  Falbesoner found was that over the years libsecp256k1 had improved
  significantly whereas OpenSSL had remained the same. He also concluded that
  outside the Bitcoin ecosystem, the secp256k1 curve is not that relevant, so it
  is not justified for OpenSSL to put too many resources into improving it
  (evident by the results). Overall, switching to libsecp256k1 was a beneficial
  decision for Bitcoin Core.

{:#restrictingdata}
- **Multiple discussions about restricting data:** ...

{:#stalerates}
- **Modeling stale rates by propagation delay and mining centralization:** ...

{:#bip3}
- **BIP3 and the BIP process:** ...

{:#kernelapi}
- **Bitcoin Kernel C API introduced:** [Bitcoin Core #30595][] introduces a C
  header that serves as an API for [`bitcoinkernel`][Bitcoin Core #27587],
  enabling external projects to interface with Bitcoin Core’s block validation
  and chainstate logic via a reusable C library. Currently, it is limited to
  operations on blocks and has feature parity with the now-defunct
  `libbitcoin-consensus` (see [Newsletter #288][news288 lib]).

  Use cases for `bitcoinkernel` include alternative node implementations, an
  Electrum server index builder, a [silent payment][topic silent payments]
  scanner, a block analysis tool, and a script validation accelerator, among
  others. Several language bindings are in development, including for
  [Rust][kernel rust], [Go][kernel go], [JDK][kernel jdk], [C#][kernel csharp],
  and [Python][kernel python].

<div markdown="1" class="callout" id="optech">

## Summary 2025: Bitcoin Optech

In Optech's eighth year, we published 50 weekly [newsletters][] and this
Year-in-Review special.  Altogether, Optech published over 80,000 English words
about Bitcoin software research and development this year, the rough equivalent
of a 225-page book.

Each newsletter and blog post was translated into Chinese, French, and Japanese,
with other languages also receiving translations, for a total of over 150
translations in 2025.

In addition, every newsletter this year was accompanied by a [podcast][]
episode, totaling over 60 hours in audio form and over 500,000 words in
transcript form.  Many of Bitcoin's top contributors were guests on the show,
some of them on more than one episode, with a total of 75 different unique
guests in 2025:

- 0xB10C
- Abubakar Sadiq Ismail (x3)
- Alejandro De La Torre
- Alex Myers
- Andrew Toth
- Anthony Towns
- Antoine Poinsot (x5)
- Bastien Teinturier (x3)
- Bob McElrath
- Bram Cohen
- Brandon Black
- Bruno Garcia
- Bryan Bishop
- Carla Kirk-Cohen (x2)
- Chris Stewart
- Christian Kümmerle
- Clara Shikhelman
- Constantine Doumanidis
- Dan Gould
- Daniela Brozzoni (x2)
- Daniel Roberts
- Davidson Souza
- David Gumberg
- Elias Rohrer
- Eugene Siegel (x2)
- Francesco Madonna
- Gloria Zhao (x2)
- Gregory Sanders (x2)
- Hunter Beast
- Jameson Lopp (x2)
- Jan B
- Jeremy Rubin (x2)
- Jesse Posner
- Johan Halseth
- Jonas Nick (x4)
- Joost Jager (x2)
- Jose SK
- Josh Doman (x2)
- Julian
- Lauren Shareshian
- Liam Eagen
- Marco De Leon
- Matt Corallo
- Matt Morehouse (x7)
- Moonsettler
- Naiyoma
- Niklas Gögge
- Olaoluwa Osuntokun
- Oleksandr Kurbatov
- Peter Todd
- Pieter Wuille
- PortlandHODL
- Rene Pickhardt
- Robin Linus (x3)
- Rodolfo Novak
- Ruben Somsen (x2)
- Russell O’Connor
- Salvatore Ingala (x4)
- Sanket Kanjalkar
- Sebastian Falbesoner (x2)
- Sergi Delgado
- Sindura Saraswathi (x2)
- Sjors Provoost (x2)
- Steve Myers
- Steven Roose (x3)
- Stéphan Vuylsteke (x2)
- supertestnet
- Tadge Dryja (x3)
- TheCharlatan (x2)
- Tim Ruffing
- vnprc
- Vojtěch Strnad
- Yong Yu
- Yuval Kogman
- ZmnSCPxj (x3)

Optech was the fortunate and grateful recipient of another $20,000 USD contribution to
our work from the [Human Rights Foundation][]. The funds will be used to pay for
web hosting, email services, podcast transcriptions, and other expenses that
allow us to continue and improve our delivery of technical content to the
Bitcoin community.

### A special thank you

After contributing as the primary author for 376 consecutive Bitcoin Optech
newsletters, Dave Harding stepped back from regular contributing this year. We
cannot thank Harding enough for anchoring the newsletter for 8 years and all of
the Bitcoin education, elucidation, and understanding he brought the community.
We are grateful and wish him well.

</div>

## December

FIXME:bitschmidty

*We thank all of the Bitcoin contributors named above, plus the many
others whose work was just as important, for another incredible year of
Bitcoin development.  The Optech newsletter will return to its regular
Friday publication schedule on January 2nd.*

<style>
#optech ul {
  max-width: 800px;
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  padding: 0;
  margin: 0;
  justify-content: center;
}

#optech li {
  flex: 1 0 220px;
  max-width: 220px;
  box-sizing: border-box;
  padding: 5px;
  margin: 5px;
}

@media (max-width: 720px) {
  #optech li {
    flex-basis: calc(50% - 10px);
  }
}

@media (max-width: 360px) {
  #optech li {
    flex-basis: calc(100% - 10px);
  }
}
</style>

{% include snippets/recap-ad.md when="2025-12-23 17:30" %}
{% include references.md %}
{% include linkers/issues.md v=2 issues="1699,1895,1974,27587,30595,31375,33629" %}
[topics index]: /en/topics/
[yirs 2018]: /en/newsletters/2018/12/28/
[yirs 2019]: /en/newsletters/2019/12/28/
[yirs 2020]: /en/newsletters/2020/12/23/
[yirs 2021]: /en/newsletters/2021/12/22/
[yirs 2022]: /en/newsletters/2022/12/21/
[yirs 2023]: /en/newsletters/2023/12/20/
[yirs 2024]: /en/newsletters/2024/12/20/

[newsletters]: /en/newsletters/
[Human Rights Foundation]: https://hrf.org
[openssl vs libsecp256k1]: /en/newsletters/2025/11/07/#comparing-performance-of-ecdsa-signature-validation-in-openssl-vs-libsecp256k1
[channel jamming results]: /en/newsletters/2025/10/24/#channel-jamming-mitigation-simulation-results-and-updates
[channel jamming resource]: https://delvingbitcoin.org/t/hybrid-jamming-mitigation-results-and-updates/1147#p-3212-resource-attacks-3
[channel jamming sink]: https://delvingbitcoin.org/t/hybrid-jamming-mitigation-results-and-updates/1147#p-3212-manipulation-sink-attack-9
[channel jamming attack]: /en/topics/channel-jamming-attacks/
[erlay optech posts]: /en/newsletters/2025/02/07/#erlay-update
[erlay]: /en/topics/erlay/
[erlay knowledge]: https://delvingbitcoin.org/t/erlay-filter-fanout-candidates-based-on-transaction-knowledge/1416
[erlay fanout amount]: https://delvingbitcoin.org/t/erlay-find-acceptable-target-number-of-peers-to-fanout-to/1420
[erlay transaction received]: https://delvingbitcoin.org/t/erlay-define-fanout-rate-based-on-the-transaction-reception-method/1422
[erlay candidate peers]: https://delvingbitcoin.org/t/erlay-select-fanout-candidates-at-relay-time-instead-of-at-relay-scheduling-time/1418
[selfish miner post]: https://delvingbitcoin.org/t/where-does-the-33-33-threshold-for-selfish-mining-come-from/1757
[selfish miner paper]: https://arxiv.org/pdf/1311.0243
[fingerprinting post]: https://delvingbitcoin.org/t/fingerprinting-nodes-via-addr-requests/1786
[bitvm3 post]: https://delvingbitcoin.org/t/garbled-circuits-and-bitvm3/1773
[delbrag rubin]: https://rubin.io/bitcoin/2025/04/04/delbrag/
[garbled circuits wiki]: https://en.wikipedia.org/wiki/Garbled_circuit
[eagen ml]: https://mailing-list.bitcoindevs.xyz/bitcoindev/Aq_-LHZtVdSN5nODCryicX2u_X1yAQYurf9UDZXDILq6s4grUOYienc4HH2xFnAohA69I_BzgRCSKdW9OSVlSU9d1HYZLrK7MS_7wdNsLmo=@protonmail.com/
[eagen paper]: https://eprint.iacr.org/2025/1485
[dahlias post]: https://mailing-list.bitcoindevs.xyz/bitcoindev/be3813bf-467d-4880-9383-2a0b0223e7e5@gmail.com/
[dahlias paper]: https://eprint.iacr.org/2025/692.pdf
[fork guide post]: https://delvingbitcoin.org/t/bitcoin-forking-guide/1451
[fork guide red]: https://ajtowns.github.io/bfg/research.html
[fork guide pue]: https://ajtowns.github.io/bfg/power.html
[fork guide ie]: https://ajtowns.github.io/bfg/industry.html
[fork guide ir]: https://ajtowns.github.io/bfg/investor.html
[template mrkt post]: https://delvingbitcoin.org/t/best-worst-case-mevil-response/1465
[mevpool gh]: https://github.com/mevpool/mevpool/blob/0550f5d85e4023ff8ac7da5193973355b855bcc8/mevpool-marketplace.md
[ln fees post]: https://delvingbitcoin.org/t/fee-based-spam-prevention-for-lightning/1524
[ln fees paper]: https://github.com/JohnLaw2/ln-spam-prevention
[swiftsync delving post]: https://delvingbitcoin.org/t/ibd-booster-speeding-up-ibd-with-pre-generated-hints-poc/1562/
[swiftsync ruben gh]: https://gist.github.com/RubenSomsen/a61a37d14182ccd78760e477c78133cd
[swiftsync rust impl]: https://delvingbitcoin.org/t/swiftsync-speeding-up-ibd-with-pre-generated-hints-poc/1562/18
[news288 lib]: /en/newsletters/2024/02/07/#bitcoin-core-29189
[kernel rust]: https://github.com/sedited/rust-bitcoinkernel
[kernel go]: https://github.com/stringintech/go-bitcoinkernel
[kernel jdk]: https://github.com/yuvicc/bitcoinkernel-jdk
[kernel csharp]: https://github.com/janb84/BitcoinKernel.NET
[kernel python]: https://github.com/stickies-v/py-bitcoinkernel
[gcc update]: /en/newsletters/2025/02/07/#updates-to-cleanup-soft-fork-proposal
[gcc bip]: /en/newsletters/2025/04/04/#draft-bip-published-for-consensus-cleanup
[news thikcs]: /en/newsletters/2025/08/01/#taproot-native-op-templatehash-proposal
[ctv csfs symmetry]: /en/newsletters/2025/04/04/#ln-symmetry
[ctv csfs arks]: /en/newsletters/2025/04/04/#ark
[ctv vaults]: /en/newsletters/2025/04/04/#vaults
[ctv dlcs]: /en/newsletters/2025/04/04/#dlcs
[lnhance update]: /en/newsletters/2025/12/05/#lnhance-soft-fork
[rubin key ladder]: https://rubin.io/bitcoin/2024/12/02/csfs-ctv-rekey-symmetry/
[ctv csfs ptlcs]: /en/newsletters/2025/07/04/#ctv-csfs-advantages-for-ptlcs
[ctv csfs bitvm]: /en/newsletters/2025/05/16/#description-of-benefits-to-bitvm-from-op-ctv-and-op-csfs
[ctv csfs letter]: /en/newsletters/2025/07/04/#open-letter-about-ctv-and-csfs
[gcc impl tests]: /en/newsletters/2025/11/07/#bip54-implementation-and-test-vectors
[ccv bip]: /en/newsletters/2025/05/30/#bips-1793
[ccv semantics]: /en/newsletters/2025/04/04/#op-checkcontractverify-semantics
[vault withdrawn]: /en/newsletters/2025/05/16/#bips-1848
[64bit bip]: /en/newsletters/2025/05/16/#proposed-bip-for-64-bit-arithmetic-in-script
[txhash sponsors]: /en/newsletters/2025/07/04/#op-txhash-variant-with-support-for-transaction-sponsorship
[txhash]: /en/newsletters/2022/02/02/#composable-alternatives-to-ctv-and-apo
[tweakadd]: /en/newsletters/2025/09/05/#draft-bip-for-adding-elliptic-curve-operations-to-tapscript
[ecmath]: /en/newsletters/2025/09/05/#draft-bip-for-adding-elliptic-curve-operations-to-tapscript
[gsr bips]: /en/newsletters/2025/10/03/#draft-bips-for-script-restoration
[transitory cleanups]: /en/newsletters/2025/01/03/#transitory-soft-forks-for-cleanup-soft-forks
[simplicity 370]: /en/newsletters/2025/09/05/#details-about-the-design-of-simplicity
[simplicity I post]: https://delvingbitcoin.org/t/delving-simplicity-part-three-fundamental-ways-of-combining-computations/1902
[simplicity II post]: https://delvingbitcoin.org/t/delving-simplicity-part-combinator-completeness-of-simplicity/1935
[simplicity III post]: https://delvingbitcoin.org/t/delving-simplicity-part-building-data-types/1956
[simplicity IV post]: https://delvingbitcoin.org/t/delving-simplicity-part-two-side-effects/2091
[simplicity V post]: https://delvingbitcoin.org/t/delving-simplicity-part-programs-and-addresses/2113
[news339 sv2fields]: /en/newsletters/2025/01/31/#bitcoin-core-31583
[news346 waitnext]: /en/newsletters/2025/03/21/#bitcoin-core-31283
[news360 checkblock]: /en/newsletters/2025/06/27/#bitcoin-core-31981
[news359 starkware]: /en/newsletters/2025/06/20/#stratum-v2-stark-proof-demo
[news369 ipc]: /en/newsletters/2025/08/29/#bitcoin-core-31802
[news374 ipcauto]: /en/newsletters/2025/10/03/#bitcoin-core-33229
[news376 30]: /en/newsletters/2025/10/17/#bitcoin-core-30-0
[news377 ipclog]: /en/newsletters/2025/10/24/#bitcoin-core-33517
[news381 witness]: /en/newsletters/2025/11/21/#bitcoin-core-33745
[news346 hashpool]: /en/newsletters/2025/03/21/#hashpool-v0-1-tagged
[news323 miningipc]: /en/newsletters/2024/10/04/#bitcoin-core-30510
[news340 richter ggt]: /en/newsletters/2025/02/07/#discovery-of-previous-research-for-finding-optimal-cluster-linearization
[news341 pr-review-club txgraph]: /en/newsletters/2025/02/14/#bitcoin-core-pr-review-club
[news352 wuille linearization techniques]: /en/newsletters/2025/05/02/#comparison-of-cluster-linearization-techniques
[news377 ismail template improvement]: /en/newsletters/2025/10/24/#detecting-block-template-feerate-increases-using-cluster-mempool
[news382 cluster mempool completed]: /en/newsletters/2025/11/28/#bitcoin-core-33629)
[news bip360 update]: /en/newsletters/2025/03/07/#update-on-bip360-pay-to-quantum-resistant-hash-p2qrh
[news qr sha]: /en/newsletters/2025/04/04/#securely-proving-utxo-ownership-by-revealing-a-sha256-preimage
[news qr cr]: /en/newsletters/2025/07/04/#commit-reveal-function-for-post-quantum-recovery
[news qr lopp1]: /en/newsletters/2025/04/04/#should-vulnerable-bitcoins-be-destroyed
[news qr lopp2]: /en/newsletters/2025/08/01/#migration-from-quantum-vulnerable-outputs
[news qr cruz]: /en/newsletters/2025/04/04/#draft-bip-for-destroying-quantum-insecure-bitcoins
[qr bip destroy]: https://github.com/chucrut/bips/blob/master/bip-xxxxx.md
[news qr corallo]: /en/newsletters/2025/01/03/#quantum-computer-upgrade-path
[rubin lamport]: https://gnusha.org/pi/bitcoindev/CAD5xwhgzR8e5r1e4H-5EH2mSsE1V39dd06+TgYniFnXFSBqLxw@mail.gmail.com/
[lamport]: https://en.wikipedia.org/wiki/Lamport_signature
[conduition sphincs]: /en/newsletters/2025/12/05/#slh-dsa-sphincs-post-quantum-signature-optimizations
[abdel stark]: /en/newsletters/2025/11/07/#native-stark-proof-verification-in-bitcoin-script
[news qr agg]: /en/newsletters/2025/11/07/#post-quantum-signature-aggregation
[news frost bip]: /en/newsletters/2024/08/09/#proposed-bip-for-scriptless-threshold-signatures
[news offchain dlc]: /en/newsletters/2025/01/24/#correction-about-offchain-dlcs
[news dlc channels]: /en/newsletters/2023/07/19/#wallet-10101-beta-testing-pooling-funds-between-ln-and-dlcs
[Cedarctic post]: /en/newsletters/2025/09/19/#partitioning-and-eclipse-attacks-using-bgp-interception
[eclipse attack]: /en/topics/eclipse-attacks/
