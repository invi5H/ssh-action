# SSH Action
A github action to setup ssh key and config in the current environment.

# Usage
```
name: ssh command
on: push
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - id: ssh
        uses: invi5H/ssh-action@v1
        with:
          SSH_HOST: ${{ secrets.SSH_HOST }}
          SSH_PORT: ${{ secrets.SSH_PORT }}
          SSH_USER: ${{ secrets.SSH_USER }}
          SSH_KEY: ${{ secrets.SSH_KEY }}
      - run: ssh ${{ steps.ssh.outputs.SERVER }} pwd
```

For multiple servers, run the above action multiple times, with a unique lowercase name each time
```
name: ssh command
on: push
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - id: ssh-foo
        uses: invi5H/ssh-action@v1
        with:
          NAME: foo
          SSH_HOST: ${{ secrets.FOO_HOST }}
          SSH_PORT: ${{ secrets.FOO_PORT }}
          SSH_USER: ${{ secrets.FOO_USER }}
          SSH_KEY: ${{ secrets.FOO_KEY }}
      - id: ssh-bar
        uses: invi5H/ssh-action@v1
        with:
          NAME: bar
          SSH_HOST: ${{ secrets.BAR_HOST }}
          SSH_PORT: ${{ secrets.BAR_PORT }}
          SSH_USER: ${{ secrets.BAR_USER }}
          SSH_KEY: ${{ secrets.BAR_KEY }}
      - run: ssh ${{ steps.ssh-foo.outputs.SERVER }} pwd
      - run: ssh ${{ steps.ssh-bar.outputs.SERVER }} pwd
```
