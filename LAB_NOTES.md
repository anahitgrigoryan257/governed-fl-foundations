# BANA 690A Federated Learning I: Lab Notes

**Name: Anahit Grigoryan**
**GitHub username:anahitgrigoryan257**

One to three sentences per prompt, in your own words, with a number from your
own run where the prompt asks for one. Commit this file to your fork by the
end of class (see README, "Turning in your notes").

## Lab 0: The world
What does the coordinator hold, and what does it never hold?
The coordinator holds 500 consented, de-identified evaluation rows per hospital, but never holds hospitals' training records or individual patients.

## Lab 1: FedAvg from scratch
Which hospital gains most from federating, by how much (your numbers), and what would you offer Northgate to join?
Kestrel gains most, rising from 0.696 to 0.798 (+10.2 percentage points). Northgate gains only 1 point despite supplying 1,800 of 2,560 patients, so I would offer it a voice in decisions and contribution-based benefit-sharing.

## Lab 2: McMahan's knobs
From the grid: which knob cuts communication rounds the most, and what do you pay for it?
Increasing E cuts rounds most: at C=1.0, E=1, 5, and 20 take 27, 6, and 2 rounds (27, 30, and 40 local epochs). Under realistic skew at C=0.34, E=5 to 20 stays at 5 rounds but raises local work from 25 to 100 epochs.

## Lab 3: Heterogeneity
Which skew hurt the most, which hospital paid, and what fixed it?
Label skew hurt Kestrel most: FedAvg accuracy was 0.730 versus 0.786 local-only, while fine-tuning raised it to 0.792. Concept shift also hurt Kestrel (0.804 versus 0.828), but fine-tuning restored it; quantity skew helped it.

## Lab 4: Vertical federation
What crossed the wire, what leaked anyway, and who should own the resulting model?
The parties exchanged partial scores and residuals: 108,000 intermediate numbers, but no feature values. Residuals exposed 100% of labels and partial scores leaked claims information, so Northgate and the insurer should jointly govern the model and its use.

## Lab 5: Threats
Finish the sentence: "FL keeps raw data at home, but ..." Then: which attack would you have caught from update norms alone, and which not?
FL keeps raw data at home, but updates can still leak patients: one gradient reconstructed features with 1.11e-16 error, and membership inference was 65% local versus 52% federated. Norms flag boost (10.37) and backdoor (8.123), but not label flipping (1.037, within the honest 0.228-1.789 range).

## Lab 6: Defenses
Which aggregator would you make the charter default, what minimum number of participants per round, and what noise multiplier for a five-hospital consortium? One sentence of justification each.
Use the coordinate-wise median: backdoor success fell to 6% with 0.817 global accuracy; compute it with secure multiparty computation to hide individual updates. Require at least three hospitals per round, since two can expose an individual update by subtraction. Start at noise multiplier 0.5 for five hospitals (0.806 accuracy versus 0.814 without noise) and verify epsilon with a privacy accountant.

## Lab 7: FL as a governance control
The charter had to choose between secure aggregation and robust aggregation. Which did you choose, what compensating control did you add, and what one clause would you add to the consortium agreement?
We chose trimmed-mean robust aggregation over secure aggregation, retaining DP noise 0.3 and a three-hospital minimum as compensating controls. The agreement should restrict update access to audited defenses, prohibit retention or reuse, and require member approval before deployment.

## Declaration
I ran these labs myself in my own Codespace. Anahit Grigoryan
