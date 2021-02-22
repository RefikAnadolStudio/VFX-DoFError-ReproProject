# VFX-DoFError-ReproProject
Test project to reproduce VFX/HDRP Depth of Field errors
 
I have identified two different visual errors with the Unity HDRP Depth of Field effect when used in conjunction with the Visual Effect Graph system. Tested on Unity 2020.1.16f1, with HDRP version 8.3.1.
 
## Error 1: Weird Bokeh 'Doubling'
![Image of weird bokeh](./dof_weirdbokeh.PNG)
![Closeup image of weird bokeh](./dof_weirdbokeh_closeup.PNG)

In some situations - seemingly when a particle is 'in between' the fully blurred out bokeh splat and 'nearly in focus' blurred states - the particle is visibly drawn directly on top of the bokeh splat. At low resolutions this looks fine, but at higher resolutions (4K, 8K, etc.) it is very obviously drawing the particle 'in focus' and the bokeh splat at the same time. This 'doubling' is not an optical phenomenon we see with real lenses; it looks weird.

Sampling at higher resolution in DoF quality settings helps, but only to an extent. The 'doubling' effect is always there. In addition, raising the DoF quality settings can cause crashes and instability; in older versions of Unity 2020.1x it can actually cause the entire DoF and HDRP stack to fail due to kernel errors (lol).

## Error 2: 'Artifacting'
![Image of artifacting](./dof_artifacting.PNG)
![Image of artifacting at 8K resolution - note the much uglier presentation](./dof_artifacting_8k.PNG)

When there are a large number of particles that are very nearly defocused, it creates a strange visual artifact that is similar to jpeg or video compression. There is a rapid change between blurred and unblurred pixels, and it looks very much like digital noise. As with the doubling issue, at lower resolutions the issue is much less noticeable, but as the resolution increases it becomes more and more apparent. And again, this effect is reduced at higher sample settings, but is always present to some extent, and raising the sampling settings causes instability.
