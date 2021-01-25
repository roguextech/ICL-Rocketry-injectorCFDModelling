# injectorCFDModelling
WIP CFD model of injectors using openFOAM 2006  
Currently using interPhaseChangeFoam, from modified cavitating bullet tutorial
This uses incompressible fluid model, as seen in CIRA paper

Literature:  
https://drive.google.com/drive/u/0/folders/1pLNUjTEDKc12vxf4TFTfJRrxMRk-E3q4  

<h1>notes</h1>
<h2>mesh</h2>
<p>
    
- roughly 98% hexahedral, 2% prisms

- generated by: 
    - creating a wedge using blockmesh
    - discarding the plate modelled in cad using SHM from the wedge
    - collapsing the faces on the wedge knife edge using collapseEdges
    - manually changing the patch types for side1 & side2 to cyclical
- so far I've used a cyclical BC, but it's possible wedge would be better


- generated by: 
    - creating a wedge using blockmesh
    - dimensions were taken from CIRA paper for Waxman case to compare results.
- mesh was updated to use wedge BC

- when finding the cells to discard, I've been using an axisymmetric wedge made in Fusion360 of the correct size etc,
    but i believe it would work just as well using an stl of the whole injector plate
    
- cell refinement near the injector is created using grading in the x direction 
- may have to use multiple blocks & merge them to create mesh similar to UoT, with defined refinement around each injector hole.
    Doing this by hand sounds mind numbing if running a decent no. of cases, a matlab or python script could automate it somewhat
</p>

<h2>turbulence</h2>
<p>

- k-omega SST turbulence was used as boundary layer was well meshed and it proviedes the most reliable results available with RANS approach.<br/>
</p>
    
<h2>cavitation</h2>
<p>
    
- currently SchnerrSauer coeffs are exactly as seen in the cavitating bullet tutorial<br/>
- can calculate these using Rayleigh–Plesset equation (see paper in literature for more details
- n_0 has to be found by testing convergence of simulation. It affects mostly where does cavitation start.<br/>
</p>
    
<h2>current models</h2>
<p>
    
- k-omega SST model was used to model turbulence<br/>
- cavitation does not match with predictions in CIRA paper, probably further refinement of mesh near intlet to injector have to be done<br/>
- to extract mass flow rate velocity field has to be integrated over section of mesh in Paraview<br/>
</p>
