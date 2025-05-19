# Forking 'tidyvcd' repository on Github

## Step 1: Fork the Repository on Github
- Went to git repo
- Clicked fork
- Git generated a copy of the repo, named it 'tidyvcd'

## Step 2:
- Open Ubuntu terminal
- Ran the command
```bash
git clone https://github.com/hpahama/tidyvcd
```

## Step 3:
-Navigate to repository
```bash
cd tidyvcd
```

## Step 4:
- Set Original repository as the upstream
```bash
git remote add upstream https://github.com/vcd2df/r.git
```

## Step 5:
- Check that both origin (fork) and upstream (original repo) are set:
```bash
git remote -v
```
------
Next:
- To fetch latest updates
    ```bash
    git fetch upstream
    ```
- To merge
    ```bash
    git merge upstream/main
    ```
- To push updates back to my fork
    ```bash
    git push origin main
    ```
