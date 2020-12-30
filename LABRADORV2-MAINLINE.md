## Caninos Loucos Labrador - Kernel Mainline

Labrador did not have support for the mainline Kernel. Caninos Loucos engineers are maintain a downstream Kernel with support for their hardware on Github: https://github.com/caninos-loucos/labrador-linux. So, I saw an opportunity to contribute to adding this support to the Linus Torvalds git tree.

I started work in February, since then there have been 7 revision on the `Linux Kernel Mainling List`, with discussions with maintainers for improvements and definitions, so finally in December this support land the Linux kernel v5.10:

![Labrador V2 Matheus Castello Kernel Linux Contributions](https://github.com/microhobby/blog/blob/master/img/labrador-contribs.png?raw=true)

> ⚠️ It is important to remember that these contributions were made without any employment bond or contract with Caninos Loucos or LSI-Tec. They were made during my free time.

### How Are Development Boards for Kernel Linux born?

> 😂 Come the stork of the boards and take a baby board at the house of the Linus Torvalds!

This was something totally new for me. It is a work process, but I will defend the processes. Without this process it would be impossible to maintain so many sub systems, architectures, millions of lines of code and guarantee the quality of the Linux Kernel. Do you have room for improvements and automation? Yep! But it is not the scope of this post.

How are boards for the Linux Kernel born? First, we have to add the board manufacturer to a list of vendor prefixes. This was the [first patch] (https://lore.kernel.org/patchwork/patch/1309977/) in the series:

> ⚠️ I'm not adding the full diff here, just a few parts to illustrate. Click on the links to see the diff and the full patch!

```diff
diff --git Documentation/devicetree/bindings/vendor-prefixes.yaml
   "^calxeda,.*":
     description: Calxeda
+  "^caninos,.*":
+    description: Caninos Loucos Program
```

As you can see I added the prefix `caninos`. This will be the prefix that we will use to make the compatible bindings with the Caninos Loucos program. So now we can document the new hardware that will be added. This was the [second patch] (https://lore.kernel.org/patchwork/patch/1309979/) in the series:

```diff
diff --git Documentation/devicetree/bindings/arm/actions.yaml 
+      - items:
+          - enum:
+              - caninos,labrador-base-m # Labrador Base Board M v1
+          - const: caninos,labrador-v2  # Labrador Core v2
+          - const: actions,s500
       - items:
           - enum:
               - lemaker,guitar-bb-rev-b # LeMaker Guitar Base Board rev. B
```

Note that as Labrador v2 consists of a computer on module and base board I had to document both that were respectively: `caninos, labrador-v2` and `caninos,labrador-base-m`.

Ok, was the board born? Calm! With the prefix of the vendor defined and new hardware documented we can then add the description of  Labrador hardware features that will be initialized by the Kernel. Adding the famous `Device Tree Source`. This was the [third patch] (https://lore.kernel.org/patchwork/patch/1309975/):

```diff
diff --git arch/arm/boot/dts/owl-s500-labrador-base-m.dts 
+/dts-v1/;
+
+#include "owl-s500-labrador-v2.dtsi"
+
+/ {
+	model = "Caninos Labrador Core v2 on Labrador Base-M v1";
+	compatible = "caninos,labrador-base-m",
+		     "caninos,labrador-v2", "actions,s500";
+
```

```diff
diff --git arch/arm/boot/dts/owl-s500-labrador-v2.dtsi 
+#include "owl-s500.dtsi"
+
+/ {
+	model = "Caninos Labrador Core V2.1";
+	compatible = "caninos,labrador-v2", "actions,s500";
+
+	memory@0 {
+		device_type = "memory";
+		reg = <0x0 0x80000000>;
```

Notice how I use the `vendor prefix` and the names documented in the `compatible` property. In the case of `owl-s500-labrador-base-m.dts` the `compatible` is  `caninos,labrador-base-m` because I am describing the hardware of the base board. In `owl-s500-labrador-v2.dtsi` the `compatible` is `caninos,labrador-v2` because I am now describing only the computer on module hardware.

Also note that there is a third level of hardware description that goes into `#include "owl-s500.dtsi"`. For a board to be born it also needs the processor description, the SoC (System on Chip). And for that it would also be necessary to add the manufacturer's vendor prefix and etc. In the case of Labrador v2 the SoC is Actions Semiconductors s500 described by `owl-s500.dtsi`. Thankfully, there were already more boards that use the s500 on mainline so I didn't have to describe the SoC's features, properties and manufacturer.

![owl-s500 device tree source hierarchy](https://github.com/microhobby/blog/blob/master/img/cyberpunl-devicetree.png?raw=true)

And with that, IT WAS BORN! Now the Linux Kernel has defined the `vendor prefix` of the Caninos Loucos program and will know what to do, which drivers to load, when booting hardware described by the Labrador v2 Device Tree Source `owl-s500-labrador-base-m.dts` maintained in mainline.

## Current Status - In Progress

For now what the device tree source of Caninos Loucos Labrador describes is the UART 3 serial port, a clock for the serial to be used as a console and ONLY THIS!! There is still a lot of work ahead, but as you may have noticed in the video at the beginning of the post, we are already booting from the eMMC and micro SD Card. But this is a spoiler, work in progress and should enter the kernel v5.12. The active community that works with the Actions Semiconductors platform on the Linux Kernel is quite small but has made a lot of progress. They are also adding support for Actions PMIC which is used in with Actions SoCs, so hopefully by 2021 we will have a mainline Kernel version ready to use with everything the board offers.

### Why is Mainline Important?

> 🤔Why have this work to add support to the Kernel Mainline if the Caninos engineers already maintain a repository on Github with a version that works well on Labrador hardware?

Let's say, hypothetically, that a new vulnerability has been discovered in the Linux kernel. In order to keep your system safe you have to update to the latest version that fixes said vulnerability. When a vulnerability is discovered, an effort is made by Kernel developers to release patches with fixes as soon as possible. And do you know where these patches are applied? In the mainline tree of the Linux kernel. In order to apply these corrections in a `downstream` Kernel you will have more work and you have to take care to be using a `LTS - Long Term Support` version, and also long-term support takes longer to reach end of life but will eventually end.  And make sure not to add modifications that are very different from the development pattern of the Linux Kernel, and always update your downstream to avoid conflicts. Without saying in the "non-critical" bug fixes that the community finds and new features added, the development of the Linux Kernel is very dynamic. It is much more laborious to maintain a downstream instead of applying an initial "bureaucratic" effort to maintain a mainline. The bureaucracy and processes of applying code to the Linux Kernel will guarantee the quality of system support for your hardware from the beginning.

> ⚠️ I'm not saying it's wrong to keep downstream. In some cases, the best way to support a platform quickly is to maintain some form of downstream. But it is important to work downstream as if you are on mainline, and strive to have exclusive downstream modifications applied to mainline as soon as possible. This will make your life much easier in the future.

## Conclusion

A priori it seems kind of silly to be so excited about a lot of little letters appearing on a screen coming from an electronic device, but I was very proud to see a project with Brazilian work being officially added to the largest free software project in the world. And I was also very happy to had the opportunity to worked on it. It is still an initial support but it is a start. We still have a lot of code ahead but we cannot give up on national projects and we have to encourage it, give feedback, test and contribute whenever possible.

### Recognition

To the people of [RoboCore] (https://www.robocore.net/) and LSI-Tec for the Labrador testing program. It was through the testing program that I got my hands on a Labrador for the first time. Also to the Actions Semi community on Kernel Mainline.
