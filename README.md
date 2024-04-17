# nh video repo

## Defining FLAKE

```nix
# configuration.nix

{ pkgs, ... }: {

  environment.sessionVariables = {
    FLAKE = "/home/username/dotfiles";
  };

  environment.systemPackages = with pkgs; [
    nh
  };
}
```

## Specialisations example

```nix
# configuration.nix

{ pkgs, ... }: {

  services.xserver.videoDrivers = ["nvidia"];
  hardware.nvidia.package =
    config.boot.kernelPackages.nvidiaPackages.production;
  
  specialisation = {
    nvidiaBeta.configuration = {
      hardware.nvidia.package =
        config.boot.kernelPackages.nvidiaPackages.beta;
      environment.etc."specialisation".text = "nvidiaBeta";
    };
    nvidiaStable.configuration = {
      hardware.nvidia.package =
        config.boot.kernelPackages.nvidiaPackages.stable;
      environment.etc."specialisation".text = "nvidiaStable";
    };
  };

}
```
