# Tournament Manager Suite

A collection of command-line tournament management tools written in Python.

## Tools

### doefish - Elimination Tournaments
Manages single and double elimination tournaments.

**Features:**
- **Double elimination** for 4 and 8 players (with losers bracket and grand finals)
- **Single elimination** for any other player count (with automatic bye handling)
- Persistent tournament storage
- Win/loss tracking and standings
- 3rd place matches

### rorofish - Round Robin Tournaments
Manages round robin league-style tournaments.

**Features:**
- **Single round robin** - each pair plays once
- **Double round robin** - each pair plays twice (home and away)
- Works with any number of players
- Point-based standings (Win=3pts, Draw=1pt, Loss=0pts)
- Automatic tiebreakers (Points → Wins → Losses)

## Installation

1. Clone this repository:
```bash
git clone https://github.com/nalanbar/doefish.git
cd doefish
```

2. Make scripts executable:
```bash
chmod +x doefish rorofish
```

3. (Optional) Add to your PATH:
```bash
# Add to ~/.bashrc or ~/.zshrc
export PATH="$PATH:/path/to/doefish"
```

## Usage

### doefish (Elimination)

**Create a tournament:**
```bash
# 4 or 8 players = double elimination
./doefish --new "Tournament Name" --players "Alice,Bob,Charlie,Diana"

# Other counts = single elimination
./doefish --new "5 Player Tourney" --players "p1,p2,p3,p4,p5"
```

**View bracket:**
```bash
./doefish --show "Tournament Name"
```

**Record match result:**
```bash
./doefish --update "Tournament Name" --match 1 --winner 1
```

**View standings:**
```bash
./doefish --standings "Tournament Name"
```

**List all tournaments:**
```bash
./doefish --list
```

**End a tournament early:**
```bash
./doefish --end "Tournament Name"
```

**Delete a tournament:**
```bash
./doefish --delete "Tournament Name"
```

### rorofish (Round Robin)

**Create a tournament:**
```bash
# Single round robin
./rorofish --new "Spring League" --players "Alice,Bob,Charlie,Diana"

# Double round robin (home and away)
./rorofish --new "Fall League" --players "p1,p2,p3,p4" --double
```

**View matches:**
```bash
./rorofish --show "Spring League"
```

**Record match result:**
```bash
# Player 1 wins
./rorofish --update "Spring League" --match 1 --winner 1

# Draw (use -1)
./rorofish --update "Spring League" --match 2 --winner -1
```

**View standings:**
```bash
./rorofish --standings "Spring League"
```

**Other commands:**
```bash
./rorofish --list                    # List all tournaments
./rorofish --end "Spring League"     # End tournament early
./rorofish --delete "Spring League"  # Delete tournament
```

## Tournament Data Storage

All tournament data is stored in `~/.tournament_data/`:
- doefish tournaments: `<name>.json`
- rorofish tournaments: `rr_<name>.json`

## Examples

### Running a 4-player double elimination tournament:
```bash
./doefish --new "Rose Lunch Feb" --players "Nabil,Richard,Tyler,Micah"
./doefish --update "Rose Lunch Feb" --match 1 --winner 1
./doefish --update "Rose Lunch Feb" --match 2 --winner 3
./doefish --show "Rose Lunch Feb"
./doefish --standings "Rose Lunch Feb"
```

### Running a round robin league:
```bash
./rorofish --new "Wednesday League" --players "Alice,Bob,Charlie,Diana,Eve"
./rorofish --show "Wednesday League"
./rorofish --update "Wednesday League" --match 1 --winner 1
./rorofish --update "Wednesday League" --match 2 --winner -1  # Draw
./rorofish --standings "Wednesday League"
```

## Tournament Types

### doefish
- **4 or 8 players:** Double elimination bracket with losers bracket, grand finals, and bracket reset if needed
- **Other counts:** Single elimination with automatic byes for top seeds, 3rd place match

### rorofish
- **Single round robin:** Each pair of players faces each other once
- **Double round robin:** Each pair plays twice (reverses home/away)
- **Standings:** Win = 3 points, Draw = 1 point, Loss = 0 points

## Requirements

- Python 3.6+
- No external dependencies (uses only standard library)

## Why "doefish" and "rorofish"?

**doefish** started as a Fish shell script for **d**ouble **e**limination tournaments. It was rewritten in Python and now supports single elimination too, but the name stuck because it's technically no longer accurate - the best kind of software naming.

**rorofish** follows the naming convention: **ro**und **ro**bin + fish suffix for consistency (and because it's fun).

## License

MIT License - feel free to use, modify, and distribute.

## Contributing

Issues and pull requests welcome! This is a personal project but happy to accept improvements.

## Author

Nabil ([@nalanbar](https://github.com/nalanbar))