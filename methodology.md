# Methodology

## Data Source(s)
- **NBA_2004_Shots.csv**  
  - Downloaded from Kaggle (publicly available historical NBA shot logs).
- **NBA_2024_Shots.csv**  
  - Downloaded from the same Kaggle repository (publicly available historical NBA shot logs).
- Both datasets include: player name, team, game ID, date, shot distance, shot type, shot result,
  coordinates, position, and position group. Also includes other data I won't be including

---

## Data Preparation / Cleaning
- **Removed header row** manually so the dataset begins with actual shot records.
- **Split each line** using `.split(",")` when converting lines to Python lists.
- **Standardized made/missed shots**:
  - Converted values in the `SHOT_MADE` column to uppercase.
  - Treated `"TRUE"` and `"1"` as made shots.
- **Normalized positions**:
  - Used `POSITION_GROUP` to classify rows into `G`, `F`, `C`, or `U`(If unknown).
- **Defined big-man shooters**:
  - Used the `POSITION` column to identify PFs and Cs.
  - Filtered only players with **≥ 50 three-point attempts**.
- **Filtered all 3PT attempts** using `SHOT_TYPE == "3PT Field Goal"`.
- **Created dictionaries** for tracking made/attempted 3PT shots per:
  - Position group
  - Player
  - Big-men shooters (PF/C)
- **Handled invalid or missing position values** by storing them as `"U"` (Unknown).
- Assumed both datasets shared identical column indices and structure.

---

## Assumptions
- **Shot classification**:
  - Assumed `"3PT Field Goal"` correctly represents actual 3-point attempts.
- **Position logic**:
  - Assumed `POSITION_GROUP` provides correct general role information, not including hybrids.
  - Used only first-letter grouping (`G`, `F`, `C`) for consistency.
- **Attempt thresholds**:
  - Required **50+ 3PT attempts** to count a big man as a meaningful shooter, despite those not existing much in 2004.
- **Dataset consistency**:
  - Assumed column formatting matched across both years.

---

## Limitations
- **Position uncertainties**:
  - Hybrid positions (F/C, G/F) may be classified inaccurately.
- **Era rules and pace not included**:
  - The dataset does not include external basketball context that affects shooting trends.
- **Curry influence inferred, not measured**:
  - No column in the data explicitly connects Curry to league-wide changes, but it's assumed from significant evidence.
- **Big-man classification may be imperfect**:
  - Some modern stretch forwards/centers may not be listed purely as PF/C in the dataset.
