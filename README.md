<img src="assets/logo.png" width="112" height="112" alt="FloorBreach logo">

# FloorBreach

Locate the first reserve breach and count all deficient period ends. This Blyx library is part of the financial data analysis collection.

A positive closing balance can conceal a mid-period reserve breach. Replay the signed flows in order. [GnuCash, cash flow reporting](https://www.gnucash.org/docs/v5/C/gnucash-manual/report-classes.html)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-floorbreach.git
cd blyx-floorbreach
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-floorbreach) · [Package page](https://www.blyx-lang.space/packages/floorbreach) · [Handbook](https://doc.blyx-lang.space/guide/siskin)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-floorbreach.git vendor/floorbreach
```

```blyx
use vendor::floorbreach::floorbreach;

fn main() {
    let opening = 20.0;
    let flows = [-15, -10, 30];
    let reserve = 10.0;
    let result = floorbreach_trace(opening, flows, reserve);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
0
2
15
```

## API

`floorbreach_trace(opening, flows, reserve)`

Returns [first deficient period, deficient periods, largest shortfall]. The opening balance initializes the trace; only period ends are counted. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| opening | A exact signed integer |
| flows | Vector of values, each a exact signed integer |
| reserve | A exact signed integer |

## In use

[Siskin](https://github.com/Rahulchaube1/blyx-siskin) uses this module to inspect a cash-flow schedule for shortfalls that disappear by the closing date.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-floorbreach/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
